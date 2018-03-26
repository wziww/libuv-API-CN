
---

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



