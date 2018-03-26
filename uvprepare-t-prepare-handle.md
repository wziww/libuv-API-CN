# uv\_prepare\_t— Prepare handle

准备句柄将在每次循环迭代中运行给定的回调，在轮询I/O之前。

## 数据类型

```
uv_prepare_t
```

准备句柄类型。

```cpp
void (*uv_prepare_cb)(uv_prepare_t* handle)
```

传递给 uv\_prepare\_start\(\) 的回调函数的类型定义。

## 共有成员

> See also
>
> The[`uv_handle_t`](http://docs.libuv.org/en/v1.x/handle.html#c.uv_handle_t)members also apply.

## API

```cpp
int uv_prepare_init(uv_loop_t* loop, uv_prepare_t* prepare)
```

handle 初始化

---

```cpp
int uv_prepare_start(uv_prepare_t* prepare, uv_prepare_cb cb)
```

以提供的回调函数启动 handle。

---

```cpp
int uv_prepare_stop(uv_prepare_t* prepare)
```

停止 handle，回调函数不再会被执行。

---

> See also
>
> The[`uv_handle_t`](http://docs.libuv.org/en/v1.x/handle.html#c.uv_handle_t)API functions also apply.



