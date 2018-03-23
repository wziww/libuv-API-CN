# uv\_loop\_t -- Event loop

> 事件循环\(Event loop\)是libuv功能的中心, libuv 提供了一套事件循环和基于I/O\(或其他活动\)通知的回调函数.

### 数据类型

**uv\_loop\_t**

```
         Loop的数据类型
```

**uv\_run\_mode**

         Loop运行方式 \(枚举类型\)  用作运行loop   _通过调用函数_[_uv\_run\(\)_](http://docs.libuv.org/en/v1.x/loop.html#c.uv_run)

```cpp
typedef enum {
    UV_RUN_DEFAULT = 0,
    UV_RUN_ONCE,
    UV_RUN_NOWAIT
} uv_run_mode;
```



