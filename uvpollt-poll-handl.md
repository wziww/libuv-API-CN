
---

# uv\_poll\_t— Poll handle

Poll handles 被用作于观察文件描述符的可读性，可写性以及断开，类似于 [poll\(2\)](https://linux.die.net/man/2/poll)。

Poll handles 的目的是让依赖于 event loop 的外部库能够在 socket 状态发生改变的时候发出信号，例如 c-ares 或者 libss2。用 uv\_poll\_t 去实现其他目的是不推荐的。uv\_tcpt，uv\_udp\_t 等等，相比较 uv\_poll\_t 而言提供了更快，更可拓展的实现，尤其是在Windows 上。



