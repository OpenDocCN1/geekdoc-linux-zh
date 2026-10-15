
# 13.7 真实世界的编程

```c
        if((ticket_array[i] != TICKET_AVAIL &&
            kill(ticket_array[i], 0) == -1) && (errno == ESRCH)) {
            /* 进程已消失 - 释放槽位 */
            printf(tick, "%d&%d&", ticket_array[i], i);
            narrate("freeing", tick, NULL);
            ticket_array[i] = TICKET_AVAIL;
            num_tickets_out--;
        }
    }
    alarm(RECLAIM_INTERVAL); /* 重置闹钟 */
}
```

接下来，我们添加代码来命名该函数，以便调度票据回收函数，并在正常处理期间关闭闹器。这个修订后的 `main` 函数出现在 `lserv2.c` 中：

```c
int main(int ac, char *av[]) {
    struct sockaddr client_addr;
    socklen_t addr=sizeof(client_addr);
    char buf[MSGLEN];
    int ret, sock;
    void ticket_reclaim(); /* 版本 2 新增内容 */
    unsigned time_left;

    sock = setup();
    signal(SIGALRM, ticket_reclaim); /* 运行票据回收器 */
    alarm(RECLAIM_INTERVAL); /* 在此延迟后 */
    while(1) {
        addrlen = sizeof(client_addr);
        ret = recvfrom(sock, buf, MSGLEN, 0, &client_addr, &addr);
        if (ret != -1) {
            buf[ret] = '0';
            narrate("GOT:", buf, &client_addr);
            time_left = alarm(0);
            handle_request(buf, client_addr, addrlen);
            alarm(time_left);
        } else if (errno != EINTR) {
            perror("recvfrom");
        }
    }
}
```

通过这些细小的添加，我们的许可证服务器会按计划回收未使用的票据。我们需要按计划回收票据吗？为什么不只在表格填满且客户端被拒绝权限时才回收票据呢？那样会更好吗？

## 13.7.2 处理服务器崩溃

服务器崩溃有两个严重的后果。首先，签出列表丢失了；没有记录哪些进程持有哪些票据。其次，没有客户端可以运行，因为授予权限的程序不可用了。显而见的解决方案是重新启动服务器（见图 13.10）。

![](img/99837708330d437de319a559cfa6cda7_456_0.png)

图 13.10
服务器崩溃后重启服务器。

重启服务器允许新客户端运行，但引入了两个新问题。第一个新问题是，重启后的服务器中的票据数组是空的；服务器拥有一组全新的、未使用的票据。崩溃服务器中的票据数组可能是满的，但这个新服务器会乐意向另一组客户端授予权限。反复地杀死并重启许可证服务器就像在印钱。

另一个新问题是，当持有之前服务器实例签发的票据的客户端释放这些票据时，他们会被告知自己持有的是假票据。

### 票据验证

解决这两个问题的方案是票据验证。票据验证意味着每个客户端都会定期向服务器发送其票据的副本。客户端发送一个数据报说：“这是我的票据。它仍然有效吗？”（见图 13.11）。

![](img/99837708330d437de319a559cfa6cda7_456_0.png)

图 13.11
客户端验证票据。

客户端发送票据和索引。服务器检查表格。流程如图 13.12 所示。

![](img/99837708330d437de319a559cfa6cda7_457_0.png)

图 13.12
客户端: VALD
服务器: GOOD OR FAIL

客户端现在发送并验证。服务器按计划进行验证。如果槽位是空的，服务器可能会签发票据。

### 票据中的票据验证

在服务器中添加票据验证需要两处修改。首先，我们添加一个验证票据的函数：

```c
/*************************************
 * do_validate
 * 验证客户端的票据
 * 从客户端接收的消息
 * Results:
 *   NOTE: 返回会被静态缓冲区覆盖
 */
static char *do_validate(char *msg) {
    int pid, slot;                /* 票据的组成部分 */
    /* msg 格式为 PID.slot - 解析并验证 */
    if (sscanf(msg, "%d.%d", &pid, &slot) == 2 && ticket_array[slot] == pid)
        return("GOOD Valid ticket");
    /* 错误的票据 */
    narrate("Bogus ticket", msg+5, NULL);
    return("FAIL invalid ticket");
}

handle_request(char *req, struct sockaddr_in *client, socklen_t addlen) {
    char *response;
    int ret;
    /* 执行并组合响应 */
    if (strncmp(req, "HELLO", 4) == 0)
        response = do_hello(req);
    else if (strncmp(req, "GBRYE", 4) == 0)
        response = do_goodbye(req);
    else if (strncmp(req, "VALD", 4) == 0)
        response = do_validate(req);
    else
        response = "FAIL invalid request";
    /* 将响应发送给客户端 */
    narrate("SAID: %s", response, client);
    ret = sendto(sd, response, strlen(response), 0, client, addlen);
    if (ret == -1)
        perror("SERVER sendto failed");
}
```

### 在协议中添加验证

我们在协议中添加验证：

```
Client: VALD
Server: GOOD OR FAIL
```

### 在客户端中添加验证

我们通过添加一个函数并在 `main` 中调用它来向客户端添加票据验证。客户端现在如图 13.12 所示。

## 13.7 测试版本 2

我们编译并测试这些客户端和服务器的新版本。测试包括杀死客户端、杀死服务器以及启动新的客户端和服务器。注意进程 ID 数字和程序输出的消息。为了测试目的，客户端睡眠两个 15 秒的间隔，服务器每 5 秒回收一次票据。测试结果如下：

```bash
$ cc 1server2.c 1server_funcs2.c dgram.c -o 1server2
$ cc 1clint2.c 1clint_funcs2.c dgram.c -o 1clint2
$ ./1server2 & # 启动服务器

- [1] $30804 & ./1clint2 & ./1clint2 & # 启动三个客户端
[2] $30805
[3] $30806
[4] $30807

SERVER: GOT HELO 30805 (10.200.75.200:1085)
SERVER: SAID: TICK 30805.0 (10.200.75.200:1085)

CLIENT [30805]: got ticket 30805.0
SuperSleep version 1.0 - Licensed Software
SERVER: GOT HELO 30806 (10.200.75.200:1086)
SERVER: SAID: TICK 30806.1 (10.200.75.200:1086)
```
