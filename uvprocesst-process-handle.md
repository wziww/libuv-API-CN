
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

uv\_process\_options\_t 函数中设置的 flags 参数

