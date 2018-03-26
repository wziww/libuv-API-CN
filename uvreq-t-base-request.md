
---

# uv\_req\_t - Base request

uv\_req\_t 是所有 libuv 请求类的基类。

结构的一致性使请求可以被转换为 uv\_req\_t。所有的 API 函数被定义为可以与任何类型的请求进行工作。

---

## 数据类型

### uv\_req\_t

libuv 请求结构基类

### uv\_any\_req

所有请求类的 Union

---

## 公有成员

```cpp
void* uv_req_t.data
```

用户自定义的数据空间。libuv 不使用。

```cpp
uv_req_type uv_req_t.type
```

请求类别的声明（只读）。

```cpp
typedef enum {
    UV_UNKNOWN_REQ = 0,
    UV_REQ,
    UV_CONNECT,
    UV_WRITE,
    UV_SHUTDOWN,
    UV_UDP_SEND,
    UV_FS,
    UV_WORK,
    UV_GETADDRINFO,
    UV_GETNAMEINFO,
    UV_REQ_TYPE_PRIVATE,
    UV_REQ_TYPE_MAX,
} uv_req_type;
```

---

## API



