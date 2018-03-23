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

