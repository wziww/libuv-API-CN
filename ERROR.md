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

\(\)bad 

