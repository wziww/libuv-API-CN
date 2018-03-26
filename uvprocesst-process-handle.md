
---

# uv\_process\_t— Process handle

Process handles 会产生一个新的进程并且让用户能够去控制它和通过它使用的流来建立一个信道。

## 数据类型

**uv\_process\_t**

进程操作类型

---

**uv\_process\_options\_t**

传递给 uv\_spawn\(\) 函数的进程建立参数

```cpp
typedef struct uv_process_options_s {
    uv_exit_cb exit_cb;
    const char* file;
    char** args;
    char** env;
    const char* cwd;
    unsigned int flags;
    int stdio_count;
    uv_stdio_container_t* stdio;
    uv_uid_t uid;
    uv_gid_t gid;
} uv_process_options_t;
```

---

```cpp
void (*uv_exit_cb)(uv_process_t*, int64_t exit_status, int term_signal)
```

没想好怎么翻译更好

---

**uv\_process\_flags**

uv\_process\_options\_t 函数中设置的 flags 参数。

```
enum uv_process_flags {
    /*
    * Set the child process' user id.
    */
    UV_PROCESS_SETUID = (1 << 0),
    /*
    * Set the child process' group id.
    */
    UV_PROCESS_SETGID = (1 << 1),
    /*
    * Do not wrap any arguments in quotes, or perform any other escaping, when
    * converting the argument list into a command line string. This option is
    * only meaningful on Windows systems. On Unix it is silently ignored.
    */
    UV_PROCESS_WINDOWS_VERBATIM_ARGUMENTS = (1 << 2),
    /*
    * Spawn the child process in a detached state - this will make it a process
    * group leader, and will effectively enable the child to keep running after
    * the parent exits. Note that the child process will still keep the
    * parent's event loop alive unless the parent process calls uv_unref() on
    * the child's process handle.
    */
    UV_PROCESS_DETACHED = (1 << 3),
    /*
    * Hide the subprocess console window that would normally be created. This
    * option is only meaningful on Windows systems. On Unix it is silently
    * ignored.
    */
    UV_PROCESS_WINDOWS_HIDE = (1 << 4)
};
```

---

**uv\_stdio\_container\_t**

每个传递给子进程的输入输出句柄或者 fd 的容器

```
typedef struct uv_stdio_container_s {
    uv_stdio_flags flags;
    union {
        uv_stream_t* stream;
        int fd;
    } data;
} uv_stdio_container_t;
```

---

**uv\_stdio\_flags**

指明输入输出流如何传递给子进程的参数

```cpp
typedef enum {
    UV_IGNORE = 0x00,
    UV_CREATE_PIPE = 0x01,
    UV_INHERIT_FD = 0x02,
    UV_INHERIT_STREAM = 0x04,
    /*
    * When UV_CREATE_PIPE is specified, UV_READABLE_PIPE and UV_WRITABLE_PIPE
    * determine the direction of flow, from the child process' perspective. Both
    * flags may be specified to create a duplex data stream.
    */
    UV_READABLE_PIPE = 0x10,
    UV_WRITABLE_PIPE = 0x20
} uv_stdio_flags;
```

## 公有成员

**uv\_process\_t.pid**

新产生的进程的 PID 。在 uv\_spawn\(\) 调用后被设置。

> Note
>
> The[`uv_handle_t`](http://docs.libuv.org/en/v1.x/handle.html#c.uv_handle_t)members also apply.

---

**uv\_process\_options\_t.exit\_cb**

进程退出后调用的回调函数。

---

**uv\_process\_options\_t.file**

被执行程序的路径。

---

**uv\_process\_options\_t.args**

命令行参数。args\[0\] 应为可执行文件的路径。在 Windows 上使用 CreateProcess （会将参数转换为字符串）会带来一些奇怪的错误。查看 uv\_process\_flags 中的 UV\_PROCESS\_WINDOWS\_VERBATIM\_ARGUMENTS。

---

**uv\_process\_options\_t.env**

新进程的环境变量。如果为 NULL 那么环境变量会与父进程一致。

---

**uv\_process\_options\_t.cwd**

子进程的当前工作路径。

---

**uv\_process\_options\_t.flags**

各种控制 uv\_spawn\(\) 运行的参数，详情查看 `uv_process_flags`。

---

**uv\_process\_options\_t.stdio\_count**

这东西啥玩意都没写，自己猜去

---

**uv\_process\_options\_t.stdio**

The stdio field points to an array of [`uv_stdio_container_t`](http://docs.libuv.org/en/v1.x/process.html#c.uv_stdio_container_t) structs that describe the file descriptors that will be made available to the child process. The convention is that stdio\[0\] points to stdin, fd 1 is used for stdout, and fd 2 is stderr。

> **Note：**On Windows file descriptors greater than 2 are available to the child process only if the child processes uses the MSVCRT runtime.

---

**uv\_process\_options\_t.uid**

巴拉巴拉巴拉巴拉

---

**uv\_process\_options\_t.gid**

Libuv 可以改变子进程的 “用户/群组 id”。只有在标记字段中设置适当的位时才会发生这种情况。

> **Note：**Windows 不支持，uv\_spawn\(\) 将会失败，返回 `UV_ENOTSUP`错误码。

---

**uv\_stdio\_container\_t.flags**

指定输入输出容器如何传递给子进程的参数。详情查看`uv_stdio_flags`。

---

**uv\_stdio\_container\_t.data**

包含传递给子进程的流或者 fd 的Union。

# API

```cpp
void uv_disable_stdio_inheritance(void)
```

禁用子进程从父进程那继承 fd / handles。产生的影响能让进程产生的子进程不意外地继承那些句柄。

建议在 fd 关闭和复制之前，在程序中尽可能地早调用该方法。

> **Note：**



