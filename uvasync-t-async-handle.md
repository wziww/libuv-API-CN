
---

# uv\_async\_t— Async handle

Async 操作允许用户“唤醒” event loop 并从另一个线程执行回调。

## 数据类型

**uv\_async\_t**

Async 操作类别

```cpp
void (*uv_async_cb)(uv_async_t* handle)
```

换递给[`uv_async_init()`](http://docs.libuv.org/en/v1.x/async.html#c.uv_async_init)的回调的类型定义。

