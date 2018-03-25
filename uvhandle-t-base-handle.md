
---

# uv\_handle\_t - Base handle

uv\_handle\_t 是所有 libuv 操作句柄种类的基础类。

结构是一致的，因此，任何 libuv  的操作句柄都可以被转换为 uv\_handle\_t 。所有的 API 函数被定义为可以和任何操作句柄类型进行工作。

Libuv 的句柄是不可移动的。传递给函数的句柄结构指针必须在所请求的操作期间保持有效。使用堆栈分配句柄时要小心。

---

## 数据类型

**uv\_handle\_t**

libuv 基础句柄类型。

**uv\_handle\_type**

libuv 操作句柄类型。

```cpp
typedef enum {
  UV_UNKNOWN_HANDLE = 0,
  UV_ASYNC,
  UV_CHECK,
  UV_FS_EVENT,
  UV_FS_POLL,
  UV_HANDLE,
  UV_IDLE,
  UV_NAMED_PIPE,
  UV_POLL,
  UV_PREPARE,
  UV_PROCESS,
  UV_STREAM,
  UV_TCP,
  UV_TIMER,
  UV_TTY,
  UV_UDP,
  UV_SIGNAL,
  UV_FILE,
  UV_HANDLE_TYPE_MAX
} uv_handle_type;
```

**uv\_any\_handle**

所有句柄类型的union

```cpp
void (*uv_alloc_cb)(uv_handle_t* handle, size_t suggested_size, uv_buf_t* buf)
```

对传递给 uv\_read\_start\_\(\) 和 \_uv\_udp\_recv\_start\(\)

## 共有成员



