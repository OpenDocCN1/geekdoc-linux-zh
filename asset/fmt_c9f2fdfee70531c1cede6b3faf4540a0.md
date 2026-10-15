
- 7. 如果不是服务器，那么它是客户端活动。如果接收到 `close`，则客户端已离开，将其从描述符集合中移除。否则，你按照之前示例中的方法“服务”客户端。

```c
else {
    ioctl(fd, FIONREAD, &nread);
    if (nread == 0) {
        close(fd);
        FD_CLR(fd, &readfds);
        printf("removing client on fd %d\n", fd);
    } else {
        read(fd, &ch, 1);
        sleep(5);
        printf("serving client on fd %d\n", fd);
        ch++;
        write(fd, &ch, 1);
    }
}
```

> 在现实程序中，建议包含一个存储已连接最大 `fd` 号的变量（不一定是最近连接的 `fd` 号）。这可以防止遍历成千上万个甚至没有连接且不可能准备就绪读取的 `fd`。我们在这里省略它仅仅是为了简洁起见，并让代码更简单。

当你运行这个版本的服务器时，它会在单个进程中按顺序处理多个客户端。

```bash
$ ./server5 &
[7] 1

$ ./server5 &
[8] 2

$ ./server5 &
[9] 3

$ ./server5 &
[10] 4
```

## Sockets

```c
servinfo = getservbyname("daytime", "udp");
if(!servinfo) {
    fprintf(stderr, "no daytime service\n\n");
    exit(1);
}
printf("daytime port is %d\n", ntohs(servinfo -> s_port));
```

```c
/* Create a UDP socket. */
```

```c
sockfd = socket(AF_INET, SOCK_DGRAM, 0);
```

```c
/* Construct the address for use sendto/recvfrom... */
address.sin_family = AF_INET;
address.sin_port = servinfo -> s_port;
address.sin_addr = (struct in_addr *)hostinfo -> h_addr_list;
len = sizeof(address);
```

```c
result = sendto(sockfd, buffer, 1, 0, (struct sockaddr *)&address, len);
result = recvfrom(sockfd, buffer, sizeof(buffer), 0,
    (struct sockaddr *)&address, &len);
```

```c
buffer[result] = '\0';
printf("read %d bytes: %s", result, buffer);
```

```c
close(sockfd);
exit(0);
```

如你所见，所需的更改非常小。与之前一样，你通过请求 `UDP` 协议来指定数据报服务。你使用 `socket` 配合 `SOCK_DGRAM` 参数创建一个数据报套字。你像以前一样设置目标地址，但现在你必须发送数据报，而不是从套字中读取。

由于你没有对 `UDP` 提供的服务建立隐式连接，你必须有某种方法让服务器知道你想接收响应。在这种情况下，你向服务发送一个数据报（在这里，你向将要接收响应的缓冲区发送一个单字节），然后它会返回日期和时间。

```c
int sendto(int sockfd, void *buffer, size_t len, int flags,
    struct sockaddr *to, socklen_t len);
```

在正常使用，`flags` 参数可以保持为 `0`。

`recvfrom` 系统调用在套字上等待来自指定地址的数据报文，并将其接收到缓冲区中。

```c
int recvfrom(int sockfd, void *buffer, size_t len, int flags,
    struct sockaddr *from, socklen_t *fromlen);
```
