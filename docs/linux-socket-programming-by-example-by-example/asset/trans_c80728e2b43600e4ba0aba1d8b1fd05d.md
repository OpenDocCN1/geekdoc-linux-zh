

## 清单 17.8：续

```
230:    if ( s == -1 )
231:        bail("socket(2)");
232:
233:    /*
234:     * Create abstract address:
235:     */
236:    memset(&a_srvr,0,sizeof a_srvr);
237:    a_srvr.sun_family = AF_LOCAL;
238:    strcpy(a_srvr.sun_path,
239:           "zSOCKET-SERVER",
240:           sizeof a_srvr.sun_path-1);
241:    a_srvr.sun_path[0] = 0;
242:
243:    /*
244:     * Bind the server address:
245:     */
246:    z = bind(s,
247:            (struct sockaddr *)&a_srvr,
248:            sizeof a_srvr);
249:    if ( z == -1 )
250:        bail("bind(2)");
251:
252:    /*
253:     * Now make this a listening socket:
254:     */
255:    z = listen(s,10);
256:    if ( z == -1 )
257:        bail("listen(2)");
258:
259:    /*
260:     * Now process requests:
261:     */
262:    for (;;) {
263:        /*
264:         * Wait for a connect:
265:         */
266:        alen = sizeof a_clnt;
267:        c = accept(s,&a_clnt,&alen);
268:        if ( c == -1 )
269:            bail("accept(2)");
270:
271:        /*
272:         * Process this request:
273:         */
274:        process_client(c,argv+1);
275:        close(c);
276:    }
277: }
278: return 0;
279: }
```

套接字服务器的清单代码相当长，因此让我们将其研究拆分成较小的片段。`main()` 程序使用的步骤如下：

- 1. 套接字服务器程序要求至少有一个命令行参数。每个参数都是被允许在端口 80 上请求套接字的用户 ID 名称（第 220 行至第 224 行）。
- 2. 创建一个 `PF_LOCAL` (`PF_UNIX`) 流式套接字，并将其绑定到一个抽象套接字地址（第 229 行至第 250 行）。
- 3. 调用 `listen(2)` 函数以允许连接到此套接字（第 255 行至第 257 行）。
- 4. 服务器循环的顶部从第 262 行的 `for` 语句开始。
- 5. 连接在第 266 行至第 269 行被接受。
- 6. 客户端程序的请求通过在第 274 行调用 `process_client()` 来处理，然后关闭客户端的套接字（第 275 行）。
- 7. 服务器继续执行步骤 4，直到服务器终止。

现在，检查 `process_client()` 函数的步骤：

- 1. 此函数接受客户端套接字 `c` 和被授予请求权限的用户 ID 列表作为输入（第 131 行至第 134 行）（此参数来自 `argv[1]`）。
- 2. 在接收到凭据之前，必须启用套接字选项 `SOL_SOCKET` 的 `SO_PASSCRED`。第 146 行至第 152 行启用了此套接字功能。
- 3. 调用函数 `recv_cred()`（清单 17.4）以接收请求和客户端的凭据（第 158 行至第 165 行）。请求返回在变量 `port` 中，这是端口号。凭据将返回在变量 `cred` 中，该变量在第 138 行声明。`recv_cred()` 程序被设计为在未接收到凭据时返回 -1。
- 4. 在请求的值为 `port`，且凭据 `cred` 可用的情况下，访问请求在函数 `check_access()`（第 171 行）中进行测试。如果指针值 `pw` 返回且不为 `NULL`，则授予访问权限。否则，拒绝访问。
- 5. 第 173 行测试指针 `pw` 是否为 `NULL`。如果不为 `NULL`，则调用函数 `grant_access()` 以响应请求。当请求成功授予时，函数在第 176 行返回给调用者。然而，如果失败（且有可能失败），错误会在第 179 行被捕获在变量 `er` 中。
- 6. 如果访问被拒绝，变量 `er` 被设置为错误代码 **EACCES**（第 185 行）。
- 7. 如果访问被拒绝或授予请求失败，则执行第 197 行至第 202 行的 `write(2)` 调用。此响应简单地将捕获在变量 `er` 中的错误代码作为正常数据发送回调用者。

现在，检查 `check_access()` 的代码：

- 1. 接受的输入值是端口号 `number`、凭据指针 `pcred` 和特权用户 ID 列表 `vuidlist`（第 16 行至第 20 行）。
- 2. 调用函数 `getpwuid()` 以查找凭据中找到的用户 ID `number`。如果在 `/etc/passwd` 数据库中未找到该值，则通过不执行第 29 行至第 38 行立即拒绝。发生这种情况时，指针 `pw` 将为 **NULL**。
- 3. 当步骤 2 成功时，执行第 33 行至第 37 行的 `for` 循环，以查看请求用户是否是特权列表的成员。如果是，则执行第 35 行的 `break` 语句。
- 4. 第 44 行至第 45 行执行进一步测试：此模块坚持只使端口 80 可用。如果请求其他任何端口，第 45 行将拒绝该请求。如果你想实验使其他端口可用，可以自定义此区域。
- 5. 第 47 行的 `return` 语句返回指针 `pw`。如果指针未被此函数中的某些条件设置为 **NULL**，则认为该用户和请求是有效的。

现在，你必须查看函数 `grant_access()` 的代码。此函数实现以下步骤：

- 1. 函数 `grant_access()` 接受客户端套接字 `c` 和被授予的端口号 `number` 作为输入（第 62 行和第 63 行）。
- 2. 在第 72 行至第 76 行创建一个 **PF_INET** **SOCK_STREAM** 套接字。
- 3. 在第 81 行至第 84 行启用套接字选项 **SO_REUSEADDR**。如果你不喜欢等待重启使用此套接字的服务器，这特别有用。
- 4. 套接字地址绑定到请求端口的 **INADDR_ANY**（第 89 行至第 92 行）。端口在第 91 行建立。
- 5. 通过在第 97 行至第 104 行调用 `bind(2)` 绑定套接字。这是需要 root 权限的地方，而服务器拥有此权限。
- 6. 绑定的套接字现在必须通过套接字 `c` 发送回客户端。这是通过在第 110 行至第 114 行调用 `send_fd()` 完成的。
- 7. 由于套接字文件描述符 `fd` 已通过套接字 `c` 发送给客户端，服务器在第 116 行将其关闭（服务器不再需要它）。
- 8. 如果在此函数中授予请求时发生任何错误，控制将跳转到标签 `errxit`（第 119 行至第 124 行）。这里捕获错误，如果套接字文件描述符已创建则将其关闭。如果失败，此函数返回值为 -1，并在 `errno` 中建立相应的错误代码（第 123 行）。

这就结束了套接字服务器模块的巡检。下一节检查 `send_fd()` 函数的代码。

## send_fd() 函数

套接字服务器调用 `send_fd()` 函数将创建并绑定的套接字发送回请求进程。清单 17.9 显示了此函数的源代码列表。

![](img/961a0296fe36074690a9847b79332eff_482_0.png)

```
Listing 17.9: sendfd.c The send_fd( ) Function
1: /* sendfd.c
2:  *
3:  * Send a file descriptor:
4:  */
5: #include "common.h"
6: 
7: /*
8:  * Send a file descriptor via socket:
9:  *
10:  * ARGUMENTS:
11:  * s      Socket to send on
12:  * fd     Open file descriptor to send
13:  * addr   Ptr to UDP address or NULL
14:  * alen   Size of addr or zero
15:  *
16:  *
17:  * RETURNS:
18:  * 0       Successful
19:  * -1      Failed: check errno
20:  */
21: int
22: send_fd(int s, int fd, void *addr, socklen_t alen) {
23:	int z;
24:	struct msghdr msg;  /* Message header */
25:	struct iovec iov[1];       /* I/O vector */
26:	struct cmsghdr *cmseg = NULL;
27:	char buf[CMSG_SPACE(sizeof fd)];
28:	int er=0;     /* "No error" code of zero */
29:
30:	/*
31:	 * Clear message areas:
32:	 */
33:	memset(&msg,0,sizeof msg);
34:	memset(buf,0,sizeof buf);
35:
36:	/*
37:	 * Supply socket address (if any):
38:	 */
39:	msg.msg_name = addr;
40:	msg.msg_namelen = alen;
41:
42:	/*
43:	 * Install our I/O vector:
44:	 */
45:	msg.msg_iov = iov;
46:	msg.msg_iovlen = 1;
47:
48:	/*
49:	 * Initialize the I/O vector to send
50:	 * the value in "er" (which is zero).
51:	 * This is done because data must be
52:	 * transmitted to send the fd.
53:	 */
54:	io[0].iov_base = &er;
55:	io[0].iov_len = sizeof er;
56:
57:	/*
58:	 * Establish control buffer:
59:	 */
60:	msg.msg_control = buf;
61:	msg.msg_controllen = sizeof buf;
62:
63:	/*
64:	 * Configure the message to send
65:	 * a file descriptor:
66:	 */
67:	cmseg = CMSG_FIRSTHDR(&msg);
68:	cmseg->cmsg_level = SOL_SOCKET;
```

