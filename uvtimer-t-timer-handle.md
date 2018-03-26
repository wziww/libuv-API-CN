
---

# uv\_timer\_t-Timer handle

Timer handles 被用作在之后发生的回调函数的调度。

## 数据类型

## uv\__timer_\_t

Timer handle 类型。

```cpp
void (*uv_timer_cb)(uv_timer_t* handle)
```

传递给 uv\__timer_\_start\(\) 的回调函数的类型定义。

## 公有成员

> 同 [uv\_handle\_t](/uvreq-t-base-request.md)

## API

```cpp
int uv_timer_init(uv_loop_t* loop, uv_timer_t* handle)
```

句柄初始化

---

```cpp
int uv_timer_start(uv_timer_t* handle, uv_timer_cb cb, uint64_t timeout, uint64_t repeat)
```

启用 timer。timeout 和 repeat 是毫秒级的。

如果 timeout 是 0，回调函数发生在下一次 event loop 的迭代中。如果 repeat 非零，回调函数发生在下一次 timeout 毫秒后，并且在

repeat 毫秒后重复执行。

> **Note：**不要更新 event loop 对于 "now" 的概念。详情查看 uv\__update_\_time\(\)函数。
>
> 如果 timer 已经被激活。它就已经是被更新的了。

---

```cpp
int uv_timer_stop(uv_timer_t* handle)
```

停止 timer。回调函数不再会被调用。

