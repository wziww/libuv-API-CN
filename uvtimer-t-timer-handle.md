
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

---

```cpp
int uv_timer_again(uv_timer_t* handle)
```

停止 timer，如果重复重启，使用 repeat 的值作为timeout，如果 timer 之前没有被 start 过，返回错误码：UV\_EINVAL。

---

```cpp
void uv_timer_set_repeat(uv_timer_t* handle, uint64_t repeat)
```

以毫秒级设置重复间隔时间，timer 将会根据该值进行定期执行。不管回调执行时间，and will follow normal timer semantics in the case of a time-slice overrun.

例如，有个 50 ms 间隔的计时器，执行了 17 ms，它将会在 33 ms 后再次执行。如果其他任务使用了超过 33 ms（在初次调用回调后），那么，这个回调会尽可能快的再次被调用。

> **Note：**If the repeat value is set from a timer callback it does not immediately take effect. If the timer was non-repeating before, it will have been stopped. If it was repeating, then the old repeat value will have been used to schedule the next timeout.

---

```cpp
uint64_t uv_timer_get_repeat(const uv_timer_t* handle)
```

获取 计时器 repeat value。

---

> See also
>
> The[`uv_handle_t`](http://docs.libuv.org/en/v1.x/handle.html#c.uv_handle_t)API functions also apply.



