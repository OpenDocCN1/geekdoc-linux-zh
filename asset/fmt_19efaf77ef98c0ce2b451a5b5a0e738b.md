
# 418 非阻塞 I/O 第 15 章

图 15.17 Initiate nonblocking connect.

## Initiate nonblocking connect

To initiate a non-blocking connection, you must set the socket to non-blocking mode before calling `connect()`. When `connect()` is called, it will return immediately with an error like `EINPROGRESS` or `EWOULDBLOCK`, indicating that the connection is proceeding in the background.

The process typically involves:
1. Creating a socket.
2. Setting the socket to non-blocking mode using `fcntl()`.
3. Calling `connect()` and handling the `EINPROGRESS` error.
4. Using `select`, `poll`, or `epoll` to wait for the socket to become writable, indicating the connection is complete.
