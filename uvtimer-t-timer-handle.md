
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



