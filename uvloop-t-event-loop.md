# uv\_loop\_t -- Event loop

> 事件循环\(Event loop\)是libuv功能的中心, libuv 提供了一套事件循环和基于I/O\(或其他活动\)通知的回调函数.

### 数据类型



**uv\_loop\_t**

             Loop的数据类型

**uv\_run\_mode**

             Loop运行方式 \(_枚举类型 \)  _用作运行loop   通过[uv\_run\(\)](http://docs.libuv.org/en/v1.x/loop.html#c.uv_run)函数

```cpp
typedef enum {
    UV_RUN_DEFAULT = 0,
    UV_RUN_ONCE,
    UV_RUN_NOWAIT
} uv_run_mode;
```



