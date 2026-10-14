
`addrinfo` 结构体字段说明：
- `ai_family`：套接字族（如 `AF_INET` 或 `AF_INET6`）。
- `ai_socktype`：套接字类型（如 `SOCK_STREAM` 或 `SOCK_DGRAM`）。
- `ai_protocol`：协议（如 `TCP` 或 `UDP`）。
- `ai_flags`：标志。
- `ai_canon`：规范主机名。
- `ai_addr`：指向 `sockaddr` 结构。
- `ai_addrlen`：地址长度。
- `ai_next`：指向下一个 `addrinfo` 结构的链表指针。

`getaddrinfo` 用于网络地址和服务的翻译。

```c
int getaddrinfo(const char *node, const char *service, const struct addrinfo *hints, struct addrinfo **res);
```

第一个函数：
```c
int getaddrinfo(const char *node, const char *service, const struct addrinfo *hints, struct addrinfo **res);
```
