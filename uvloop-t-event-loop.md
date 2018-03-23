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

  这个操作当前仅支持SIGPROF信号. 使用sampling profiler去抑制不必要的唤醒. 使用其他信号量将会以 UV\_EINVAL

        作为失败的返回.



