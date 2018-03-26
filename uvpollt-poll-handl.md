
---

# uv\_poll\_t— Poll handle

Poll handles 被用作于观察文件描述符的可读性，可写性以及断开，类似于 [poll\(2\)](https://linux.die.net/man/2/poll)。

Poll handles 的目的是让依赖于 event loop 的外部库能够在 socket 状态发生改变的时候发出信号，例如 c-ares 或者 libss2。

