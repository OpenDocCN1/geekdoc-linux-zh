
## 15.7 传递描述符

```c
#include "unp.h"
int main(int argc, char **argv) {
    int fd;
    if (argc != 4)
        exit_err("usage: %s <filename> <mode>\n", argv[0]);
    if ((fd = my_open(argv[2], atoi(argv[3]))) < 0)
        exit(1);
    exit(0);
}
```

图 15.12 `openfile`：传递描述符。

我们的函数 `read_fd` 现在返回流管道上的描述符。除了描述符，我们还读取了一字节的数据，但并未对其进行任何操作。

在跨流管道发送和接收描述符时，我们始终至少发送一字节数据，即使接收方对数据不进行任何处理。否则，接收方会认为 `read_fd` 返回 0 意味着“没有数据（但可能有描述符）”——“文件结束”。

图 15.13 `write_fd`：通过辅助数据或访问权限传递描述符。

## 15.8 接收发送者凭据

在图 14.13 中，我们展示了另一种可以沿 Unix 域套字字的辅助数据（ancillary data）传递的数据：用户凭据。凭据具体封装并作为辅助数据发送的方式取决于操作系统。我们在这里描述 FreeBSD，其他 Unix 变体也类似（挑战在于确定应该使用哪种结构来表示凭据）。我们在此描述了这一点，尽管它在不同系统间并不统一，但它是 Unix 协议中一个重要且简洁的扩展。当客户端和服务器使用这些协议进行通信时，服务器通常需要一种方式来确切知道客户端是谁，以验证客户端是否有权限请求所请求的服务。

FreeBSD 通过 `cmscred` 结构传递凭据，该结构通过包含 `<socket.h>` 头文件定义。

```c
struct cmscred {
    pid_t  cmscred_pid;          /* 发送进程的 PID */
    uid_t  cmscred_uid;          /* 发送进程的真实 UID */
    uid_t  cmscred_euid;         /* 发送进程的有效 UID */
    gid_t  cmscred_gid;          /* 发送进程的真实 GID */
    short cmscred_ngroups;      /* 组数 */
    gid_t  cmscred_groups[CMGROUP_MAX]; /* 组 */
};
```

通常，`CMSGROUP_MAX` 为 16。`cmscred_ngroups` 至少为 1，数组的第一个元素是有效组 ID。

这些信息在 Unix 域上总是可用的，尽管发送者通常必须进行某些特殊安排以便在发送时包含这些信息，接收者通常也需要某些特殊安排（例如套接字选项）来获取凭据。在我们 FreeBSD 系统上，接收者除了调用 `recvmsg` 并提供一个足够容纳凭据的辅助缓冲区外不需要做任何特殊操作，正如图 15.14 所示。然而，发送者在发送数据时必须包含一个 `cmscred` 结构；虽然 FreeBSD 要求发送者包含该结构，但其内容是由内核填充的，发送者无法伪造。这使得通过 Unix 域套接字传递凭据成为验证客户端身份的可靠方法。

### 示例

作为凭据传递的示例，我们修改了 Unix 域流套接字来请求客户端的凭据。图 15.14 显示了一个新函数 `read_cred`，它类似于 `read`，但返回一个包含发送者凭据的 `cmscred` 结构。

- 前三个参数与 `read` 相同，第四个参数指向一个将被填充的 `cmscred` 结构指针。

- 如果返回了凭据，将对辅助数据的长度、级别和类型进行验证；如果没有返回凭据，我们将该结构设置为 0。由于组数（`cmcred_ngroups`）始终为 1 或更多，值 0 向调用者指示内核没有返回凭据。

我们回显服务器的主函数（图 15.3）保持不变。图 15.15 显示了 `str_echo` 函数的新版本，该函数是根据图 5.3 修改而来的。该函数在父进程接受了新客户端连接并调用 `fork` 后，由子进程调用。

如果返回了凭据，则将其打印出来。循环的其余部分保持不变。这段代码从客户端读取缓冲区并将其写回客户端。

来自图 15.4 的客户端仅经过极小的修改，在调用 `sendmsg` 时传递一个空的 `msgcmdred` 结构以供填充。

```c
#include <unp.h>
#define CONTROL_LEN (sizeof(struct msgcmdred) + sizeof(struct msgcmdred))
size_t
read_creds(int fd, void *ptr, size_t nbytes, struct msgcmdred *msgcmdred)
{
    struct msgcmdred;
    struct iovec iov[1];
    char control[CONTROL_LEN];
    int n;
    msg.msg_name = NULL;
    msg.namelen = 0;
    iov[0].base = ptr;
    iov[0].len = nbytes;
    msg.msg_iov = iov;
    msg.msg_iovlen = 1;
    msg.msg_control = control;
    msg.msg_controllen = sizeof(control);
    msg.msg_flags = 0;

    if ((n = recvmsg(fd, &msg, 0)) < 0)
        return (n);

    msgcmdptr->msg_creds.ngroups = 0; /* 表示未返回凭据 */
    if (msgcmdptr->msg_creds.control > 0) {
        struct msgcmdred *cmptr = (struct msgcmdred *)control;
        if (cmptr->msg_len < CONTROL_LEN)
            err_quit("control length = %d", cmptr->msg_len);
        if (cmptr->msg_level != SOL_SOCKET)
            err_quit("control level = ! SOL_SOCKET");
        if (cmptr->msg_type != SCM_CREDS)
            err_quit("control type = ! SCM_CREDS");
        memcpy(msgcmdptr, CMSG_DATA(cmptr), sizeof(struct msgcmdred));
    }

    return (n);
}
```

图 15.14 `read_creds` 函数：读取并返回发送者的凭据。

```c
#include "unp.h"

size_t read_cred(int, void *, size_t, struct cmscred *)

void
str_echo(int sockfd)
{
    ssize_t n;
    int i;
    char buf[MAXLINE];
    struct cmscred cred;

again:
    while ((n = read_cred(sockfd, buf, MAXLINE, &cred)) > 0) {
        if (cred.ngroups > 0) {
            printf("PID: %d, UID: %d, EUID: %d, GID: %d, groups: %d\n",
                cred.cmscred_pid, cred.cmscred_uid, cred.cmscred_euid,
                cred.cmscred_gid, cred.cmscred_ngroups);
        } else {
            printf("No credentials returned\n");
        }
        if (write(sockfd, buf, n) != n)
            err("write");
    }
    if (n < 0 && errno == EINTR)
        goto again;
    else if (n < 0)
        err("str_echo: error");
}
```

## 15.9 总结
