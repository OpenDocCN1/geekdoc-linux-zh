
```c
/* cli.c - 客户端，面向连接型模型 */
#include "sc.h"

int main(void) {
    int sock_fd;
    struct sockaddr_un unix_addr;
    char buf[2048];
    int n;
    if ((sock_fd = socket(AF_UNIX, SOCK_STREAM, 0)) < 0) {
        perror("cli: socket()\n");
        exit(1);
    }

    unix_addr.sun_family = AF_UNIX;
    strcpy(unix_addr.sun_path, SERVER);
    if (connect(sock_fd, (struct sockaddr*)&unix_addr,
        sizeof(unix_addr.sun_family) + strlen(unix_addr.sun_path)) < 0) {
        perror("cli: connect()");
        exit(1);
    }

    sprintf(buf, "Hello Server, this is %d.\n", getpid());

    n = strlen(buf) + 1;

    if (write(sock_fd, buf, n) != n) {
      perror("cli: write()");
      exit(1);
    }

    if ((n = read(sock_fd, buf, 2047)) < 0) {
      perror("cli: read()");
      exit(1);
    }

    buf[n] = '\0';
    printf("Client received: %s\n", buf);

    exit(0);
}
```

第一个 `socket` 描述符通过 `socket(0)` 创建。然后生成服务器的地址；在我们的示例中是 `/tmp/server`。客户端随后尝试使用 `connect(0)` 与服务器建立连接。如果成功，就可以向服务器发送数据。确切地说，客户端通过发送“Hello Server, this is [进程号]”来实现。为了让服务器回复，我们需要几行 C 程序。

```c
/* srv.c - 服务器，面向连接型模型 */
#include <signal.h>
#include "sc.h"

void stop() {
    unlink(SERVER);
    exit(0);
}

void server(void) {
    int sock_fd, cli_sockfd;
    struct sockaddr_un unix_addr;
    char buf[2048];
    int n, addr_len;
    pid_t pid;
    char *pc;

    signal(SIGINT, stop);
    signal(SIGTERM, stop);
    if ((sock_fd = socket(AF_UNIX, SOCK_STREAM, 0)) < 0) {
        perror("srv: socket()");
        exit(1);
    }

    unix_addr.sun_family = AF_UNIX;
    strcpy(unix_addr.sun_path, SERVER);
    addr_len = sizeof(unix_addr.sun_family) + strlen(unix_addr.sun_path);

    if (bind(sock_fd, (struct sockaddr *)&unix_addr, addr_len) < 0) {
      perror("srv: bind()");
      exit(1);
    }
    if (listen(sock_fd, 5) < 0) {
      perror("srv: listen()");
      exit(1);
    }

    while ((cli_sockfd = accept(sock_fd, (struct sockaddr*)&unix_addr, &addr_len)) >= 0) {
      if ((n = read(cli_sockfd, buf, 2047)) < 0) {
        perror("srv: read()");
        close(cli_sockfd);
        continue;
      }

      buf[n] = '\0';
      for (pc = buf; *pc != '\0' && (*pc < '0' || *pc > '9'); pc++) {
        // 跳过非数字字符
      }
      // 简单的逻辑来提取进程号
      pid = atoi(pc);
      printf(buf, "Hello Client %d, this is the Server.\n", pid);
      n = strlen(buf) + 1;
      if (write(cli_sockfd, buf, n) != n) {
        perror("srv: write()");
      }
      close(cli_sockfd);
      perror("srv: accept()");
    }
}

int main(void) {
    int r;
    if ((r = fork()) == 0) {
        server();
    }
    if (r < 0) {
        perror("srv: fork()");
        exit(1);
    }
    exit(0);
}
```

服务器调用 `fork()` 并终止其运行。子进程在后台运行并安装中断信号的处理程序。一旦 `socket` 文件描述符被打开，服务器自身的地址就会绑定到该 `socket`，并在地址给出的路径下创建一个文件。通过限制该文件的访问权限，服务器可以减少与其通信的用户数。客户端的 `connect` 调用只有在此文件存在且客户端拥有必要的访问权限时才会成功。调用 `listen()` 是为了通知内核该进程现在准备好接受连接。它可以调用 `accept()` 等待。如果客户端使用 `connect(0)` 建立了连接，`accept(0)` 将返回一个新的文件描述符。这将被用于从客户端接收消息并对其进行回复。服务器只需写入：

`Hello Client [进程号], this is the Server.`

服务器关闭该连接的文件描述符并再次调用 `accept()` 为下一个客户端提供服务。

`read` 和 `write` 操作在没有数据或缓冲区没有剩余空间时通常会在 `socket` 描述符上阻塞。如果设置了 `O_NONBLOCK` 标志，这些函数就不会阻塞。

从 2.0 版本开始，可以在 `LINUX` 无连接模式下使用 `UNIX` 域 `socket`，这意味着 `send()` 和 `recvfrom()`。

## 5.6.2 UNIX 域 socket 的实现

`socket` 在内核中由 `socket` 数据结构表示。`socket` 中包含的数据存储在 `skbuf` 结构中。这些在第8章中描述。

有一系列 `socket` 特有的函数，如 `socket` 和 `setsockopt()`。它们都通过一个系统调用 `socketcall` 实现，该调用通过引用第一个参数来调用所有必要的函数。文件操作 `read()`、`write()`、`select()`、`ioctl()`、`lseek()`、`close()` 和 `fasync()` 由文件描述符操作直接调用。

所有 `socket` 操作都使用包含在 `socket` 结构的操作向量 `proto_ops` 中的协议特定函数。这里简要描述了 `UNIX` 域 `socket` 操作的语义。

```c
int sys_socket(int family, int type, int protocol);
```

这设置了一个 `socket` 描述符。该函数调用了协议操作 `unix_proto_create()`，设置与 `sock` 结构相同的 `unix_socket` 结构并创建 `skbuf` 列表。此函数可能会阻塞。在完成此操作后，`socket` 的状态为 `SS_UNCONNECTED`。

```c
int sys_bind(int fd, struct sockaddr *umaddr, int addlen);
```

地址 `umaddr` 被绑定到 `socket`。协议操作自然会测试地址是否属于 `UNIX` 地址族并尝试设置套接地址文件并以写权限打开，只有当套接地址文件尚未被任何程序绑定时，`bind` 才会成功。
