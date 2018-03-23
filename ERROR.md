# 错误处理\(Error handling\)

在libuv中 错误\(errors\)是以常量形式形式出现的,根据经验，当出现一个状态参数，或者API函数返回了一个整数，这个常量表示了一个错误\(error\)。

当一个函数返回了一个错误，这个函数的回调函数永远不会被调用。

# 注意：

```
实现细节:在Unix上 错误信号为一个负常量，在windows上他们为libuv定义的任意否定的数字
```

## 错误常量

##### UV\_E2BIG

参数列表过长\(argument list too long\)

##### UV\_EACCES

权限拒绝\(permission denied\)

**UV\_EADDRINUSE**

地址已被使用\(address already in use\)

**UV\_EADDRNOTAVAIL**

地址不可用\(address not available\)

**UV\_EAFNOSUPPORT**

地址族不被支持\(address family not supported\)

**UV\_EAGAIN**

资源暂不可用\(resource temporarily unavailable\)

**UV\_EAI\_ADDRFAMILY**

地址族不被支持\(address family not supported\)

**UV\_EAI\_AGAIN**

暂时失败\(temporary failure\)

**UV\_EAI\_BADFLAGS**

ai\_flags值有误\(bad ai\_flags value\)

**UV\_EAI\_BADHINTS**

无效的hints值\(invalid value for hints\)

**UV\_EAI\_CANCELED**

请求取消\(request canceled\)

**UV\_EAI\_FAIL**

永久失败（permanent failure）

**UV\_EAI\_FAMILY**

ai族不被支持\(ai\_family not supported\)

**UV\_EAI\_MEMORY**

内存不足\(out of memory\)

**UV\_EAI\_NODATA**

没有地址\(no address\)

**UV\_EAI\_NONAME**

未知的节点或服务\(unknown node or service\)

**UV\_EAI\_OVERFLOW**

参数buffer溢出\(argument buffer overflow\)

**UV\_EAI\_PROTOCOL**

未知的解决协议\(resolved protocol is unknown\)

**UV\_EAI\_SERVICE**

服务不支持该socket类别\(service not available for socket type\)

**UV\_EAI\_SOCKTYPE**

socket类别不支持\(socket type not supported\)

**UV\_EALREADY**

连接已存在\(connection already in progress\)

**UV\_EBADF**

错误的文件描述符\(bad file descriptor\)

**UV\_EBUSY**

资源忙碌或被锁\(resource busy or locked\)

**UV\_ECANCELED**

操作取消\(operation canceled\)

**UV\_ECHARSET**

无效的Unicode字符\(invalid Unicode character\)

**UV\_ECONNABORTED**

软件造成连接终止\(software caused connection abort\)

**UV\_ECONNREFUSED**

连接拒绝\(connection refused\)

**UV\_ECONNRESET**

对等点连接复位\(connection reset by peer\)

**UV\_EDESTADDRREQ**

缺少目标地址\(destination address required\)

**UV\_EEXIST**

文件已存在\(file already exists\)

**UV\_EFAULT**

错误地址在系统调用参数中\(bad address in system call argument\)

**UV\_EFBIG**

文件过大\(file too large\)

**UV\_EHOSTUNREACH**

主机无法访问\(host is unreachable\)

**UV\_EINTR**

系统调用中断\(interrupted system call\)

**UV\_EINVAL**

无效参数\(invalid argument\)

**UV\_EIO**

I/O错误\(i/o error\)

**UV\_EISCONN**

socket连接已存在\(socket is already connected\)

**UV\_EISDIR**

对目录的非法操作\(illegal operation on a directory\)

**UV\_ELOOP**

过多的符号链接\(too many symbolic links encountered\)

**UV\_EMFILE**

过多的打开文件\(too many open files\)

**UV\_EMSGSIZE**

信息过长\(message too long\)

**UV\_ENAMETOOLONG**

名称过长\(name too long\)

**UV\_ENETDOWN**

网络中断\(network is down\)

**UV\_ENETUNREACH**

网络不可达\(network is unreachable\)

**UV\_ENFILE**

文件表溢出\(file table overflow\)

**UV\_ENOBUFS**

没有可用 buffer空间\(no buffer space available\)

**UV\_ENODEV**

没有这样的设备\(no such device\)

**UV\_ENOENT**

文件或目录不存在\(no such file or directory\)

**UV\_ENOMEM**

内存不足\(not enough memory\)

**UV\_ENONET**

设备不在网络中\(machine is not on the network\)

**UV\_ENOPROTOOPT**

协议不可用\(protocol not available\)

**UV\_ENOSPC**

设备空间不足\(no space left on device\)

**UV\_ENOSYS**

函数未实现\(function not implemented\)

**UV\_ENOTCONN**

socket未连接\(socket is not connected\)

**UV\_ENOTDIR**

不是一个目录\(not is directory\)

**UV\_ENOTEMPTY**

目录不为空\(directory not empty\)

**UV\_ENOTSOCK**

在非socket上进行的socket操作\(socket operation on non-socket\)

**UV\_ENOTSUP**

操作在socket上不被支持\(operation not supported on socket\)

**UV\_EPERM**

操作不被允许\(operation not permitted\)

**UV\_EPIPE**

断开的管道\(broken pipe\)

**UV\_EPROTO**

协议错误\(protocol error\)

**UV\_EPROTONOSUPPORT**

协议不支持\(protocol not supported\)

**UV\_EPROTOTYPE**

socket的协议类型错误\(protocol wrong type for socket\)

**UV\_ERANGE**

结果过大\(result too large\)

**UV\_EROFS**

只读文件系统\(read-only file system\)

**UV\_ESHUTDOWN**

不能在传输终端关闭后进行发送\(cannot send after transport endpoint shutdown\)

**UV\_ESPIPE**

无效的寻找\(invalid seek\)

...

# API

### uv\_strerror

```cpp
const char* uv_strerror(int err)
```

返回传入的错误码代表的错误信息.

当使用未定义的错误码时, 会泄露几个bytes的内存.

```cpp
uv_strerror(UV_EEXIST);
//file already exists
```

### uv\_err\_name

```cpp
const char* uv_err_name(int err)
```

返回传入错误码的错误名称.

当使用未定义的错误码时, 会泄露几个bytes的内存.

```cpp
uv_err_name(UV_EEXIST);
//EEXIST
```

### uv\_translate\_sys\_error

```cpp
int uv_translate_sys_error(int sys_errno)
```

返回 libuv 错误代码相当于特定平台相关的错误代码, Unix 上 POSIX 错误码\(储存在 error 中\), Windows 上 Win32错误码\(由 GetLastError\(\) 或者 WSAGetLastError\(\)方法得到\).

```cpp
uv_translate_sys_error(UV_EEXIST);
//-17
```

如果 _sys\_errno _已经是一个 libuv 错误 ,他将直接返回.

> Changed: v1.10.0 中声明为public函数



