# uv\_pipe\_t— Pipe handle

Pipe handle 在 Unix 本地域套接字和 Windows 命名管道上提供了一个抽象概念。

`uv_pipe_t`是`uv_stream_t`的子类。

# 数据类型

**uv\_pipe\_t**

Pipe handle 类

# 公有成员

> See also
>
> The[`uv_stream_t`](http://docs.libuv.org/en/v1.x/stream.html#c.uv_stream_t)members also apply.

# API

```cpp
int uv_pipe_init(uv_loop_t* loop, uv_pipe_t* handle, int ipc)
```

pipe handle 初始化。IPC参数是一个布尔值，用于表示此管道是否将用于进程间的句柄传递。

---

```cpp
int uv_pipe_open(uv_pipe_t* handle, uv_file file)
```

以管道模式打开一个存在的文件描述符或句柄。

1.2.1 版本改为：文件描述符被设置为非阻塞模式。

> **Note：传递的文件描述符或句柄没有对类型进行校验，不过需要它们为一个有效的管道。**

---

```cpp
int uv_pipe_bind(uv_pipe_t* handle, const char* name)
```

将管道绑定到文件路径（UNIX）或名称（Windows）。

> **Note：Unix 上的路径被转换为 **sizeof\(sockaddr\_un.sun\_path\) **bytes 大小 ，范围通常在 92 - 108 bytes。**

---

```cpp
int uv_pipe_getsockname(const uv_pipe_t* handle, char* buffer, size_t* size)
```

获取 Unix域套接字或命名管道的名称。

A preallocated buffer must be provided. The size parameter holds the length of the buffer and it’s set to the number of bytes written to the buffer on output. If the buffer is not big enough`UV_ENOBUFS`will be returned and len will contain the required size.

Changed in version 1.3.0:the returned length no longer includes the terminating null byte, and the buffer is not null terminated.

