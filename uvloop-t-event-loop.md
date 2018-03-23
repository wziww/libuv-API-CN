
---

# uv\_loop\_t -- Event loop

> 事件循环\(Event loop\)是 libuv 功能的中心，libuv 提供了一套事件循环和基于I/O\(或其他活动\)通知的回调函数。

## 数据类型

#### **uv\_loop\_t**

Loop的数据类型

#### **uv\_run\_mode**

Loop**运行方式** \(枚举类型\)  用作运行loop   通过调用函数 **uv\_run\(\)**

```cpp
typedef enum {
    UV_RUN_DEFAULT = 0,
    UV_RUN_ONCE,
    UV_RUN_NOWAIT
} uv_run_mode;
```

#### void \(\*uv\_walk\_cb\)\(uv\_handle\_t\* handle, void\* arg\)

传递给 uv\_walk\(\) 的回调函数的类型定义

### Public members

#### void\*uv\_loop\_t.data

用户定义数据的空间。libuv 不会使用并且不会干预这块区域

## API

```cpp
int uv_loop_init(uv_loop_t* loop)
```

初始化给定的 `uv_loop_t`结构

```cpp
uv_loop_t *loop = new uv_loop_t();
uv_loop_init(loop);
```

---

```cpp
int uv_loop_configure(uv_loop_t* loop, uv_loop_option option, ...)
```

新增于 1.0.2 版本

loop配置函数 需在 第一次调用uv\_run\(\) 前调用 除非额外提及

成功的时候返回值为 0，失败的时候返回值为 UV\_E\* 错误码。准备好处理UV\_ENOSYS，它意味着loop option 不被平台支持。

### Supported options:

* **UV\_LOOP\_BLOCK\_SIGNAL: **在轮询新事件时阻塞信号，uv\_loop\_configure\(\) 函数的第二个参数就是信号量。

  这个操作当前仅支持SIGPROF信号。使用sampling profiler去抑制不必要的唤醒。使用其他信号量将会以 [UV\_EINVAL](/ERROR.md)

  作为失败的返回。

---

```cpp
int uv_loop_close(uv_loop_t* loop)
```

释放所有 loop 资源, 只有在 loop 执行完毕, 所有打开的句柄和请求都已关闭时才调用此函数,  否则会返回 UV\_EBUSY 信号. 当该函数结束后, 用户可以释放分配给 loop 的内存.

---

```cpp
uv_loop_t* uv_default_loop(void)
```

该函数返回一个初始好的默认loop, 当分配失败的时候会返回 **NULL**

该函数是获得在整个应用中全局性 loop 的一个便捷方法, 默认的 loop 与通过调用 uv\_loop\_\_\_init\(\) 生成的 loop 是没啥不同的, 默认

loop 可以\(并且应该\)通过 uv\_loop\_close\(\) 来关闭， 因此可以释放分配给它的资源。

```css
Warning:该函数不是线程安全的
```

> nodejs中使用了默认的loop作为自己的主loop。如果你在编写nodejs的绑定，你应该注意一下。
>
> 引用自 [https://luohaha.github.io/Chinese-uvbook/source/basics\_of\_libuv.html](https://luohaha.github.io/Chinese-uvbook/source/basics_of_libuv.html)

---

```cpp
int uv_run(uv_loop_t* loop, uv_run_mode mode)
```

该函数运行 event loop 。根据不同的指定模式会采取不同的执行方式:

* **UV**\_**RUNDEFAULT:      **event pool 将会运行直到没有更多的活动引用句柄或请求。返回non-zero 如果调用了 uv\_stop\(\) 并且仍然有活动引用句柄或者请求，其他情况返回 zero。

* **UV\_RUN\_ONCE:          **轮询 I/O 一次. 注意, 该函数**会被**阻塞如果没有等待执行的回调函数. 当执行完毕后返回 zero \(没有活动引用句柄或者请求\), non-zero 当仍然有回调函数等待被执行\(意味着你以后需要应该再次运行 event pool \)。

* **UV\_RUN\_NOWAIT:     **轮询 I/O 一次. 但当没有待执行的回调时, **不会被**阻塞. 当结束时\(没有活动引用句柄或者请求\)返回 zero ，non-zero 当仍然有回调函数等待被执行\(意味着你以后需要应该再次运行 event pool \)。

---

```cpp
int uv_loop_alive(const uv_loop_t* loop)
```

当 loop 中仍有活动引用句柄, 活跃的请求 或者 正在关闭句柄的时候, 返回一个non-zero。

---

```cpp
void uv_stop(uv_loop_t* loop)
```

停止 event loop，让 uv\_run\(\) 能够尽快结束，发生于**不早于**下次 loop 迭代。如果该函数调用发生在 I/O 阻塞之前，loop 将不会在此次迭代中发生阻塞。

---

```cpp
size_t uv_loop_size(void)
```

返回 uv\_loop\_t 结构的大小. 对于不想知道该结构设计的 FFI binding writers 非常有用

---

```cpp
int uv_backend_fd(const uv_loop_t* loop)
```

获取 backend 文件描述符。 仅支持 kqueue,epoll 和 event ports。

可与 uv\_run\_\(loop,UV\_RUN\_NOWAIT\) 结合使用在一个线程中轮询，其他中执行 event loop 的回调. 案例可看 test/test-embed.c文件。

```ruby
Note: 嵌入一个 kqueue fd 进 另一个 kqueue pollset 并不能在所有平台都能正常使用. 这不是一个添加 fd 的错误 它从不生成 events.
```

---

```cpp
int uv_backend_timeout(const uv_loop_t* loop)
```

获取轮询超时时间. 返回值以毫秒为单位, 或者如果没有超时的话返回 -1。

---

```cpp
uint64_t uv_now(const uv_loop_t* loop)
```

返回当前时间戳\(毫秒级\)。时间戳会在轮询开始的时候被缓存，详情及原因查看 uv\_update\_time\(\)

时间戳从某个任意时间点单调递增。不要对出发点做假设，得到的只会是个失望结果。

```ruby
Note: 使用 uv_hrtime() 如果需要获得的亚毫秒时间
```

---

```cpp
void uv_update_time(uv_loop_t* loop)
```

更新 event loop 的对于"当前"的时间概念。Libuv 在event loop 轮询开始的时候缓存当前时间一遍减少时间相关的系统的调用次数。

你通常不需要调用此函数，除非你有回调阻塞 event loop 较长时间，“长”在某种程度上是主观的，但可能是毫秒或以上的顺序。

---

```cpp
void uv_walk(uv_loop_t* loop, uv_walk_cb walk_cb, void* arg)
```

在轮询中传递句柄，walk\_cb 将会被执行（arg为提供参数）。

