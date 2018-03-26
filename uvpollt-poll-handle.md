# uv\_poll\_t— Poll handle

Poll handles 被用作于观察文件描述符的可读性，可写性以及断开，类似于 [poll\(2\)](https://linux.die.net/man/2/poll)。

Poll handles 的目的是让依赖于 event loop 的外部库能够在 socket 状态发生改变的时候发出信号，例如 c-ares 或者 libss2。用 uv\_poll\_t 去实现其他目的是不推荐的。uv\_tcpt，uv\_udp\_t 等等，相比较 uv\_poll\_t 而言提供了更快，更可拓展的实现，尤其是在Windows 上。

有可能 poll handles 会偶尔表示一个文件描述符为可读或可写的（当它不可的时候）。所以用户应该处理巴拉巴拉。

对于一个 socket 有多个活动的句柄的行为是十分不好的，可能会导致 libuv 变为 busyloop 或者失灵。

用户不应该关闭一个文件描述符，当它被活跃的句柄轮询的时候，这会导致 handle 报错，也可能会让另一个 socket 开始轮询，

fd 可以通过调用 uv\_poll\_stop\(\) 或者 uv\_close\(\) 来进行安全的立刻关闭。

## 数据类型

uv\_poll\_t

poll 的操作类型。

