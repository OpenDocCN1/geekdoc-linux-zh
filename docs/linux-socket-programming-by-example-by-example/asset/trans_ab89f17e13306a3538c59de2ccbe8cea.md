
### 清单 14.1：续

```c
34:		putc('\n',stderr);
35:		exit(1);
36:	}
37:
38:	/*
39:	 * Call socket(2), bind(2),
40:	 * listen(2) and accept(2);
41:	 *
42:	 * Returns socket.
43:	 */
44:	int
45:	BindAccept(char *addr) {
46:		int z;
47:		int s;
48:		struct sockaddr_in adr_svr;
49:		struct sockaddr_in adr_clnt;
50:		int len_inet;
51:
52:		/*
53:		 * Create a TCP/IP socket to use:
54:		 */
55:		s = socket(PF_INET,SOCK_STREAM,0);
56:		if ( s == -1 )
57:			bail("socket()");
58:
59:		/*
60:		 * Bind the server address:
61:		 */
62:		len_inet = sizeof adr_svr;
63:		z = mkaddr(&adr_svr,&len_inet,
64:			addr,"tcp");
65:
66:		if ( z != 0 ) {
67:			puts("Bad address/port");
68:			exit(1);
69:		}
70:
71:		/*
72:		 * Bind server address:
73:		 */
74:		z = bind(s,(struct sockaddr *)&adr_svr,
75:			len_inet);
76:		if ( z == -1 )
77:			bail("bind(2)");
78:
79:		/*
80:		 * Set listen mode:
81:		 */
82:		if ( listen(s,10) == -1 )
83:			bail("listen(2)");
84:
85:		/*
86:		 * Wait for a connect:
87:		 */
88:		len_inet = sizeof adr_clnt;
89:
90:		z = accept(s,
91:			(struct sockaddr *)&adr_clnt,
92:			&len_inet);
93:
94:		if ( z == -1 )
95:			bail("accept(2)");
96:
97:		close(s);	/* No longer needed */
98:		return z;	/* Connected socket */
99:	}
100:
101:	int
102:	Connect(char *addr) {
103:	int z;
104:	int s;
105:	struct sockaddr_in adr_srvr;
106:	int len_inet;
107:
108:	/*
109:	 * Create a TCP/IP socket to use:
110:	 */
111:	s = socket(PF_INET,SOCK_STREAM,0);
112:	if ( s == -1 )
113:		bail("socket()");
114:
115:	/*
116:	 * Bind the server address:
117:	 */
118:	len_inet = sizeof adr_srvr;
119:	z = mkaddr(&adr_srvr,&len_inet,
120:		addr,"tcp");
121:
122:	if ( z != 0 ) {
123:		puts("Bad address/port");
124:		exit(1);
125:	}
126:
127:	/*
128:	 * Connect to server:
129:	 */
130:	len_inet = sizeof adr_srvr;
131:
132:	z = connect(s,
133:		(struct sockaddr *)&adr_srvr,
134:		len_inet);
135:
136:	if ( z == -1 )
137:		bail("connect(2)");
138:
139:	return s;   /* Connected socket */
140:	}
```

该模块中的主要组件包括

- `bail()` 函数，用于报告错误并中止程序（第 27 至 36 行）。
- `BindAccept()` 函数，它创建一个套接字，并将地址绑定到该套接字。此外，调用 `listen(2)` 和 `accept(2)` 以等待客户端连接。返回值是已连接的客户端套接字（第 44 至 99 行）。
- `Connect()` 函数，它创建一个套接字并连接到远程服务器（第 101 至 140 行）。

由于您现在应该已经很好地掌握了其中包含的操作，因此本源模块将不会详细讨论。

`mkrdr.c` 源模块再次沿用上一章的版本，未作任何更改，因此此处不再重复列出。

## 使用 SIGURG 信号接收

既然枯燥的基础工作已经完成，现在是时候探索这个带外数据（out-of-band data）概念的乐趣了。清单 14.2 中的程序用于接收数据，并在带外数据到达时对其进行处理。该程序专为 BSI（Berkeley Socket Interface）对带外处理的解释而设计，这是 Linux 的默认方式。

![](img/961a0296fe36074690a9847b79332eff_376_0.png)

### 清单 14.2：oobrecv.c 接收主程序

```c
1: /* oobrecv.c:
2:  *
3:  * Example OOB receiver:
4:        */
5:    #include <stdio.h>
6:    #include <unistd.h>
7:    #include <stdlib.h>
8:    #include <errno.h>
9:    #include <string.h>
10:   #include <signal.h>
11:   #include <fcntl.h>
12:   #include <sys/types.h>
13:   #include <sys/socket.h>
14:
15:   extern void bail(char *on_what);
16:   extern int BindAccept(char *addr);
17:
18:   static int s = -1;  /* Socket */
19:
20:   /*
21:    * SIGURG signal handler:
22:    */
23:   static void
24:   sigurg(int signo) {
25:       int n;
26:       char buff[256];
27:
28:       n = recv(s,buff,sizeof buff,MSG_OOB);
29:       if ( n < 0 )
30:           bail("recv(2)");
31:
32:       buff[n] = 0;
33:       printf("URG '%s' (%d)\n",
34:           buff,n);
35:
36:       signal(SIGURG,sigurg);
37:   }
38:
39:   int
40:   main(int argc,char **argv) {
41:       int z;        /* Status */
42:       char buff[256];
43:
44:
45:       /*
46:        * Use a server address from the command
47:        * line, if one has been provided.
48:        * Otherwise, this program will default
49:        * to using the arbitrary address
50:        * 127.0.0.1;
51:        */
52:       s = BindAccept(argc >= 2
53:            ? argv[1]
54:            : "127.0.0.1:9011");
55:
56:       /*
57:        * Establish ownership:
58:        */
59:       z = fcntl(s, F_SETOWN, getpid());
60:       if ( z == -1 )
61:           bail("fcntl(2)");
62:
63:       /*
64:        * Catch SIGURG:
65:        */
66:       signal(SIGURG, sigurg);
67:
68:       for (;;) {
69:           z = recv(s,buff,sizeof buff,0);
70:           if ( z == -1 )
71:               bail("recv(2)");
72:
73:           if ( z == 0 )
74:               break;
75:           buff[z] = 0;
76:
77:           printf("rcv '%s' (%d)\n",
78:               buff, z);
79:       }
80:
81:       close(s);
82:       return 0;
83:   }
```

`oobrecv.c` 主程序由以下主要部分组成：

- 一个 `SIGURG` 信号处理程序（第 23 至 37 行）
- 主测试程序（第 40 至 82 行）

首先检查主程序的功能。主程序使用的基本步骤如下：

1. 创建、绑定、监听并接受来自客户端程序的连接（第 52 至 54 行）。`BindAccept()` 函数在此处为我们处理了所有繁琐的工作。
2. 通过调用 `fcntl(2)` 建立套接字 `s` 的所有权（第 59 至 61 行）。你可以将此理解为表达接收 `SIGURG` 信号的兴趣。
3. 信号 `SIGURG` 的默认操作是忽略它。因此，必须在第 66 行建立一个信号处理程序。
4. 在第 68 行启动一个接收 `for` 循环。
5. 调用 `recv(2)` 函数接收正常数据（第 69 至 71 行）。注意这里的 `flags` 参数为零。
6. 测试套接字的文件末尾（第 72 和 73 行）。如果返回零字节，`break` 语句将跳出 `for` 循环。
7. 报告数据内容和长度（第 74 至 77 行）。
8. 重复步骤 4。

简而言之，主程序初始化并等待连接。当客户端连接时，它简单地循环接收并报告它所能接收到的每个数据块。

现在，将注意力转向信号处理程序。用于它的步骤如下：

1. 进入处理程序时，代码尝试读取一些紧急（带外）数据（第 28 至 30 行）。
2. 报告带外数据（第 32 至 34 行）。
3. 重新建立 `SIGURG` 的信号处理程序。这是必要的，因为当捕获该信号时，该信号会恢复为被忽略的状态。

> 通常，在信号处理程序中使用诸如 `printf(3)` 这样的函数是不明智的。在精心构造的条件下，像这里那样为了演示目的使用它是足够安全的。
>
> 此外，修改 `errno` 也是不明智的，例如 `recv(2)` 调用可能会做的那样。生产质量的代码应该在信号处理程序中保存并恢复 `errno` 的值，以保持其可重入性状态。

> 应该指出，在现代程序中应不鼓励使用 `signal(2)` 函数。相反，应使用可靠的信号函数，如 `sigaction(2)`。这里使用 `signal(2)` 函数是为了保持示例程序简单。

不过，在您使用接收程序之前，您需要一个发送程序。

## 发送带外数据

清单 14.3 中的程序说明了一个简短的程序，它将传输几个小字符串和一小段带外数据。该程序使用多次调用 `sleep(3)` 来管理接收端传输块的时序。

![](img/961a0296fe36074690a9847b79332eff_380_0.png)

### 清单 14.3：obsend.c 发送程序

```c
1: /* obsend.c:
2:  *
3:  * Example OOB sender:
4:  */
5: #include <stdio.h>
6: #include <unistd.h>
7: #include <stdlib.h>
8: #include <errno.h>
9: #include <string.h>
10: #include <sys/types.h>
11: #include <sys/socket.h>
12:
13: extern void bail(char *on_what);
14: extern int Connect(char *addr);
15:
16: /*
17:  * Send in-band data:
18:  */
19: static void
20: iband(int s,char *str) {
21: int z;
22:
23: z = send(s,str,strlen(str),0);
24: if ( z == -1 )
25: bail("send(2)");
26:
27: printf("ib: '%s' (%d)\n",str,z);
28: }
29:
30: /*
31:  * Send out-of-band data:
32:  */
33: static void
34: oband(int s,char *str) {
35: int z;
36:
37: z = send(s,str,strlen(str),MSG_OOB);
38: if ( z == -1 )
39: bail("send(2)");
40:
41: printf("OOB '%s' (%d)\n",str,z);
42: }
```

