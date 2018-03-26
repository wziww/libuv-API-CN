
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



