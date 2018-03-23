# uv\_loop\_t -- Event loop

> 事件循环\(Event loop\)是libuv功能的中心, libuv 提供了一套事件循环和基于I/O\(或其他活动\)通知的回调函数.

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

传递给uv\_walk\(\)的回调函数的类型定义

### Public members

#### void\*uv\_loop\_t.data

用户定义数据的空间. libuv 不会使用并且不会干预这块区域

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

成功的时候返回值为 0 ，失败的时候返回值为 UV\_E\* 错误码. 准备好处理UV\_ENOSYS; 它意味着loop option 不被平台支持.

### Supported options:

* **UV\_LOOP\_BLOCK\_SIGNAL: **在轮询新事件时阻塞信号,uv\_loop\_configure\(\) 函数的第二个参数就是信号量.

  这个操作当前仅支持SIGPROF信号. 使用sampling profiler去抑制不必要的唤醒. 使用其他信号量将会以 [UV\_EINVAL](/ERROR.md)

  作为失败的返回.

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

loop 可以\(并且应该\)通过 uv\_loop\_close\(\) 来关闭， 因此可以释放分配给它的资源.

```css
Warning:该函数不是线程安全的.
```

> nodejs中使用了默认的loop作为自己的主loop。如果你在编写nodejs的绑定，你应该注意一下。
>
> 引用自 [https://luohaha.github.io/Chinese-uvbook/source/basics\_of\_libuv.html](https://luohaha.github.io/Chinese-uvbook/source/basics_of_libuv.html)

---

```cpp
int uv_run(uv_loop_t* loop, uv_run_mode mode)
```

该函数运行 event loop .根据不同的指定模式会采取不同的执行方式:

* **UV**\_**RUNDEFAULT: **event pool 将会运行直到没有更多的活动引用句柄或请求. 返回non-zero 如果调用了 uv\_stop\(\) 并且仍然有活动引用句柄或者请求, 其他情况返回 zero.
* **UV\_RUN\_ONCE: **轮询I/O一次. 注意, 该函数会被锁住如果没有等待执行的回调函数. 当执行完毕后返回zero\(没有活动引用句柄或者请求\), non-zero 当仍然有回调函数等待被执行\(意味着你以后需要应该再次运行 event pool\).

 

