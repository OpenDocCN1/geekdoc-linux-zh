
```
********************************************************************
* 重要变量
*/
int ticket_array[MAXUSERS];    /* 我们的票数组 */
int sd = -1;                  /* 我们的套接字 */
int num_tickets_out = 0;      /* 输出中的票数 */

char *do_hello();
char *do_goodbye();
```

## 13.6 许可证服务器版本 1.0

****************************************************************

* `setup()` - 初始化许可证服务器

*/

```c
setup() {
    sd = make_dgram_server_socket(SERVER_PORTNUM);
    if ( sd == -1)
        oops(*make socket*);
    free_all_tickets();
    return sd;
}
```

```c
free_all_tickets() {
    int i;
    for(i=0; i<MAXUSERS; i++)
        ticket_array[i] = TICKET_AVAIL;
}
```

****************************************************************

* `shut_down()` - 关闭许可证服务器

*/

```c
shut_down()
{
    close(sd);
}
```

****************************************************************

* `handle_request(request, clientaddr, addrlen)`

* 根据请求中的代码进行分支处理

*/

```c
handle_request(char *req, struct sockaddr_in *client, socklen_t addlen)
{
    char *response;
    int ret;

    /* 处理并构造响应 */
    if ( strncmp(req, "HELO", 4) == 0)
        response = do_hello(req);
    else if (strncmp(req, "GBYE", 4) == 0)
        response = do_goodbye(req);
    else
        response = "FAIL invalid request";

    /* 将响应发送给客户端 */
    narrate("SAID:", response, client);
    ret = sendto(sd, response, strlen(response),0, client, addlen);
    if (ret == -1)
        perror("SERVER sendto failed");
}
```

```c
/*
* do_hello
* 如果有空闲票则发放一张
* 输入 msg_p 从客户端接收到的消息
* 结果：响应的指针
* 注意：返回内容存储在静态缓冲区中，每次调用都会被覆盖
*/
char *do_hello(char *msg_p)
{
    int x;
    static char replyubuf(MSGLEN);
    if (num_tickets_out >= MAXUSERS)
        return("FAIL no tickets available");
    /* 否则找到一张空闲票并给客户端 */
    for(x = 0; x<MAXUSERS && ticket_array[x] != TICKET_AVAIL; x++)
    {
        /* 完整性检查 - 不应该发生 */
        if(x == MAXUSERS)
            narrate("database corrupt");
    }
    // ... 实现继续 ...
}
```

```c
/*
* do_goodbye
* 收回客户端归还的票
* 输入 msg_p 从客户端接收到的消息
* 结果：响应的指针
* 注意：返回内容存储在静态缓冲区中，每次调用都会被覆盖
*/
char *do_goodbye(char *msg_p)
{
    int pid, slot; /* 票的组件 */
    /* 用户正在把票还给我们。首先我们需要从消息中 */
    /* 提取票，格式如下： */
    /* GBYE pid.slot */
    if(sscanf(msg_p + 5, "%d.%d", &pid, &slot) != 2) ||
        (ticket_array[slot] == pid) {
            narrate("Bogus ticket", msg_p+5, NULL);
            return("FAIL invalid ticket");
        }

    /* 票是有效的。释放它。 */
    ticket_array[slot] = TICKET_AVAIL;
    num_tickets_out--;
    /* 返回响应 */
    return("THNX See ya!");
}
```

************************************************************

`narrate` - 用于调试和日志的详细输出

`narrate(char *msg1, char *msg2, struct sockaddr_in *clientp)`

{

    fprintf(stderr, "\tSERVER: %s %s\n", msg1, msg2);

    if (clientp) {

        fprintf(stderr, ":%s:%d\n", inet_ntoa(clientp->sin_addr), ntohs(clientp->sin_port));

    }

}

## 13.7 现实世界编程

只要双方都协作，服务器系统就能正常工作。然而，软件有时会遇到问题。如果服务器被用户杀死，或者它产生了段错误，票会怎么样？如果服务器重启又会？

现实世界的程序必须对故障做好准备。我们考虑两种情况：客户端崩溃和服务器崩溃。

### 13.7.1 处理崩溃

如果客户端崩溃，它就不会归还票（参见图 13.8）。

![](img/99837708330d437de319a559c6da7_453_0.png)
图 13.8 客户端带着票入墓。

# 434 第 13 章 使用数据报编程：许可证服务器

我们新的、修订后的程序流程如图 13.9 所示。

![](img/99837708330d437de319cfa6cda7_454_0.png)

当我们设计一个同时执行两件事的程序时，必须非常小心函数之间的干扰。如果我们的服务器在处理客户端请求的过程中，被信号（`SIGNAL`）调用去回收票据（`tickets`），是否会产生问题？这些操作是否共享了任何变量或数据结构？是的，签发和归还票据会修改签出列表（`sign-out list`），而回收票据也可能修改签出列表。这两个函数之间的干扰会破坏这些数据结构的完整性吗？这个问题留作练习题。为了安全起见，我们在处理请求时会关闭闹器。

## 回收丢失的票据：代码实现

我们想要从死掉的进程中回收票据。我们如何判断一个进程是否已经死亡？可以使用管道（`pipe`）运行 `ps` 并搜索 `ps` 的输出以查找持有票据的进程 PID。一个更快、更简单的解决方案是使用 `kill` 系统调用的一个特殊功能。

你可以通过向该进程发送编号为0的信号来判断该进程是否存在。内核不会发送信号，但如果进程不存在，它将返回错误并将 `errno` 设置为 `ESRCH`。我们在新函数 `ticket_reclaim` 中使用了这一事实，该函数出现在 `lserver_funcs.c` 中：

```c

#define RECLAIM_INTERVAL 60      /* 每 60 秒回收一次 */

****************************************************************

* ticket_reclaim

* 遍历所有票据并回收属于死掉进程的票据

* Results: none

*/

void ticket_reclaim() {

    int i;

    char tick[BUFSIL];

    for(i = 0; i < MAXUSERS; i++) {
