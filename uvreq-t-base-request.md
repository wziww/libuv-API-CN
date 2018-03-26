
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

```cpp
int uv_cancel(uv_req_t* req)
```

取消等待中的请求。如果请求已经或者正在执行，将会失败。

成功返回 0，失败返回小于 0 的一个错误码。

当前支持取消的请求为：uv\_fs\_t，uv\_getaddrinfo\_t，uv\_getnameinfo\_t，和 uv\_work\_t。

取消请求的回调发生在之后的某个时间。在回调函数被调用之前释放相关内存是不安全的。

下面是取消函数的回调报告方式：

* uv\_fs\_t 请求将它的req-&gt;result 设置为 UV_\_ECANCELED。_
* uv\_work\_t，uv\_getaddrinfo\_t_ 或者 \_c:type:uv\_getnameinfo\_t_ 请求具有状态调为 _UV_\_ECANCELED 的回调函数。

---

```cpp
size_t uv_req_size(uv_req_type type)
```

返回给定请求类型的大小，对..FFI....特别有用。

