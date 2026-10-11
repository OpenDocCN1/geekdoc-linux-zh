

Connection closed by foreign host.

$ 确保在 IP 地址 127.0.0.1 后面指定协议号 13（你可以使用远程 IP 地址，但为了本测试过程，请坚持使用 127.0.0.1）。如果你的 daytime 服务正在运行，你应该看到显示一个日期和时间字符串，随后是消息“Connection closed by foreign host.”。

如果服务不可用，你将看到类似的输出：

![](img/961a0296fe36074690a9847b79332eff_192_0.png)

```
$ telnet 127.0.0.1 13
Trying 127.0.0.1...
telnet: Unable to connect to remote host: Connection refused
$
```

如果你看到这种情况，这表明你的 daytime 服务没有运行。要排查此问题，请检查你的 /etc/inetd.conf 文件：

![](img/961a0296fe36074690a9847b79332eff_192_1.png)

```
$ grep daytime /etc/inetd.conf
# Echo, discard, daytime, and chargen are used
#daytime stream tcp nowait root internal
#daytime dgram udp wait root internal
$
```

如本例所示，文件中 daytime 服务条目的第一列有一个 # 字符。这实际上相当于将服务“注释掉”，使其不可用。这可能是出于防止来自互联网或其他网络中恶意用户攻击的预防措施（禁用任何你认为不需要的互联网服务是一个普遍原则）。为了尝试客户端示例程序，你需要启用 tcp daytime 服务条目（如果 udp 服务条目已被注释，可以保持其注释状态不变）。

要修复服务，请编辑文件 /etc/inetd.conf，移除包含 tcp 协议的 daytime 条目开头的 # 字符。再次使用 grep 检查，你应该看到如下内容：

![](img/961a0296fe36074690a9847b79332eff_192_2.png)

```
$ grep daytime /etc/inetd.conf
# Echo, discard, daytime, and chargen are used
daytime stream tcp nowait root internal
daytime dgram udp wait root internal
$
```

在对 /etc/inetd.conf 文件进行更改后，你必须告诉 inetd 守护进程重新读取并处理已更改的文件。操作如下：

![](img/961a0296fe36074690a9847b79332eff_192_3.png)

```
$ su -
Password:
# ps ax | grep inetd
313 ? S 0:00 inetd
828 pts/1 S 0:00 grep inetd
# kill -1 313
#
```

### **注意**

如今，像 kill 命令这样的命令中正推广使用符号化信号名称。使用这些符号化信号名称的一个原因是为了安全，防止打字错误。例如，命令 `kill -1 313` 可以输入为：

```
kill -HUP 313
```

一些用户（包括作者）倾向于“冒险行事”，抵制了这种改变。

上述会话完成了以下操作：

- 1. 使用 su 命令切换到 root 账户。
- 2. 然后你找出 inetd 守护进程的进程 ID。示例中的 ps 命令表明 inetd 守护进程的进程 ID 为 313（你的进程 ID 可能不同）。
- 3. 使用 kill -1 313 命令向进程 ID 313（你的进程 ID 可能不同）发送 SIGHUP 信号。务必不要忘记命令行中的 -1（或 -HUP）参数。否则，你会杀掉你的 inetd 守护进程！

完成所有这些后，你现在应该能够重复 telnet 测试并验证其是否正常工作。

### **daytime 客户端程序**

列表 7.7 中显示的节目执行了以下简单步骤：

- 1. 查找 tcp 协议的 daytime 服务。
- 2. 使用 tcp 连接到你的 PC 的 daytime 服务器。
- 3. 读取服务器发送回你的套接字的日期和时间字符串。
- 4. 向你的终端会话报告日期和时间字符串。
- 5. 关闭套接字并返回 shell。

列表 7.7 中的客户端程序如下所示。

![](img/961a0296fe36074690a9847b79332eff_193_0.png)

### **列表 7.7：** daytime.c—客户端 daytime 演示程序

```
1: /* daytime.c:
2:  *
3:  * Example daytime client:
4:  */
5: #include <stdio.h>
6: #include <unistd.h>
7: #include <stdlib.h>
8: #include <errno.h>
9: #include <string.h>
10: #include <sys/types.h>
11: #include <sys/socket.h>
12: #include <netinet/in.h>
13: #include <arpa/inet.h>
14: #include <netdb.h>
15:
16: /*
17:  * This function reports the error and
18:  * exits back to the shell:
19: */
20: static void
21: bail(const char *on_what) {
22:     fputs(strerror(errno),stderr);
23:     fputs(": ",stderr);
24:     fputs(on_what,stderr);
25:     fputc('\n',stderr);
26:     exit(1);
27: }
28:
29: int
30: main(int argc,char **argv) {
31:     int z;
32:     char *srvr_addr = NULL;
33:     struct sockaddr_in addr_srvr;/* AF_INET */
34:     int len_inet;                 /* Length  */
35:     int s;                       /* Socket  */
36:     struct servent *sp;         /* Service entry */
37:     char dtbuf[128];            /* Date/Time info */
38:
39: /*
40:  * Use a server address from the command
41:  * line, if one has been provided.
42:  * Otherwise, this program will default
43:  * to using the arbitrary address
44:  * 127.0.0.1:
45: */
46: if ( argc >= 2 ) {
47:     /* Addr on cmdline: */
48:     srvr_addr = argv[1];
49: } else {
50:     /* Use default address: */
51:     srvr_addr = "127.0.0.1";
52: }
53:
54:     /*
55:      * Lookup the daytime tcp service:
56:      */
57:     sp = getservbyname("daytime", "tcp");
58:     if ( !sp ) {
59:         fputs("Unknown service: daytime tcp\n",
60:               stderr);
61:         exit(1);
62:     }
63:
64:     /*
65:      * Create a server socket address:
66:      */
67:     memset(&adr_srvr, 0, sizeof adr_srvr);
68:     adr_srvr.sin_family = AF_INET;
69:     adr_srvr.sin_port = sp->s_port;
70:     adr_srvr.sin_addr.s_addr =
71:         inet_addr(srvr_addr);
72:
73:     if ( adr_srvr.sin_addr.s_addr == INADDR_NONE )
74:         bail("bad address.");
75:
76:     len_inet = sizeof adr_srvr;
77:
78:     /*
79:      * Create a TCP/IP socket to use:
80:      */
81:     s = socket(PF_INET, SOCK_STREAM, 0);
82:     if ( s == -1 )
83:         bail("socket()");
84:
85:     /*
86:      * Connect to the server:
87:      */
88:     z = connect(s, &adr_srvr, len_inet);
89:     if ( z == -1 )
90:         bail("connect(2)");
91:
92:     /*
93:      * Read the date/time info:
94:      */
95:     z = read(s, &dbuf, sizeof dbuf-1);
96:     if ( z == -1 )
97:         bail("read(2)");
98:
99:     /*
100:  * Report the Date & Time:
101:  */
102:       dtbuf[z] = 0;  /* null terminate string */
103:
104:       printf("Date & Time is: %s\n", dtbuf);
105:
106:       /*
107:        * Close the socket and exit:
108:        */
109:       close(s);
110:       putchar('\n');
111:
112:       return 0;
113:  }
```

该程序可以更详细地描述如下：

- 1. 如果命令行提供了 IP 地址，程序将使用该 IP 地址（第 48 行），否则默认使用你的本地主机（也称为 localhost），使用本地环回地址 127.0.0.1（第 51 行）。命令行上的 IP 地址允许用户测试另一台远程主机上的 daytime 服务。如果在本地主机上关闭了该服务但在其他地方可用，这特别有用。
- 2. 第 57 行查找通过 TCP/IP 使用的 daytime 互联网服务。如果找不到此服务，问题将在第 59 行至第 61 行报告。
- 3. 服务器地址和地址长度在第 67 行至第 76 行建立。特别注意第 69 行，其中建立了 daytime 服务的服务端口号。
- 4. 套接字在第 81 行创建。特别注意参数 SOCK_STREAM，它指定我们要一个 TCP/IP 套接字（与 PF_INET 一起使用时）。
- 5. 程序在第 88 行连接到服务器。如果失败，错误将在第 90 行处理。
- 6. 第 95 行显示 read(2) 调用，检索服务器的输出。返回值指示读取的字节数。否则，错误将在第 97 行处理。
- 7. 第 102 行确保有一个终止空字节，以便缓冲区 dtbuf[] 可以像 C 字符串一样处理。
- 8. 第 104 行报告服务器返回的值。
- 9. 套接字在第 109 行关闭。

