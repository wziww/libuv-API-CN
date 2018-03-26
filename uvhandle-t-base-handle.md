
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

```cpp
uv_loop_t* uv_handle_t.loop
```

指向句柄正在运行的 uv\_loop\_t 的指针。 \(只读\)

---

```cpp
uv_handle_type uv_handle_t.type
```

uv\_handle\_type，指示底层句柄的类型。\(只读\)

---

```cpp
void* uv_handle_t.data
```

用户定义的数据的存储空间。libuv 不使用这个区域。

## API

```cpp
int uv_is_active(const uv_handle_t* handle)
```

当句柄是活跃的时候返回 non-zero，不活跃时返回 zero。 “活跃”状态的定义依赖于句柄的类型：

* uv\_async\_t_ _句柄总是活跃的，并且不能被“不活跃化”，通过 uv\_close\(\) 来关闭。

* uv\_pipe\_t，uv\_tcpt，uv\_udp\_t 等等。基础的 I/O 操作在进行 I/O  的时候，例如读、写、连接、接受新连接等等的时候，是活跃的。

* uv\_check\_t，uv\_idle\_t，uv\_timert 等等。当调用 uv\_check\_start\(\)，uv\_idle\_start\(\)等方法启用的时候，是活跃的。

规则：当句柄类似 uv\_foo\_t 有类似 uv\_foo\_start\(\) 函数的，当它从该函数被调用的时候被激活\(活跃\)，同样的，通过调用uv\_foo\_stop\(\)来进行让它不再活跃\(反活跃\)。

---

```cpp
int uv_is_closing(const uv_handle_t* handle)
```

句柄为正在关闭或者已关闭的时候返回 non-zero，否则返回 zero。

> **Note：该函数只应在句柄初始化之后和关闭之前调用。**

---

```cpp
void uv_close(uv_handle_t* handle, uv_close_cb close_cb)
```

句柄关闭函数，close\_cb（回调）会在该函数调用后被异步调用。

