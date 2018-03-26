
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

## 公有成员

> See also
>
> The[`uv_handle_t`](http://docs.libuv.org/en/v1.x/handle.html#c.uv_handle_t)members also apply.

## API

```cpp
int uv_async_init(uv_loop_t* loop, uv_async_t* async, uv_async_cb async_cb)
```

初始化 async 操作 ，可以提供为 NULL 的callback。

返回值：成功返回 0，失败返回小于 0 的错误码。

> **Note：**和其他初始化函数不同的是，该初始化立刻执行句柄。

---

```cpp
int uv_async_send(uv_async_t* async)
```

唤醒 event loop 并调用 async 的回调函数。

返回值：成功返回0，失败返回小于 0 的错误码。

> **Note：**线程安全，回调会在 loop 的线程被调用。

> **Warning：**libuv 会把所有 calls 聚合，因此不是所有的回调都会执行，例如，如果调用5次该方法（在回调执行之前），那么回调只会执行一次，如果再毁掉执行完后再次调用 uv\_async\_send\(\)，那么这个回调会被又一次调用。

---

> See also
>
> The[`uv_handle_t`](http://docs.libuv.org/en/v1.x/handle.html#c.uv_handle_t)API functions also apply.



