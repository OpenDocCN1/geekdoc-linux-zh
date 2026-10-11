
## 通过 `get_tickinfo()` 获取报价信息

```c
108: extern int extract_params(
109: 	Parm *plist, short n, char *src);
110: extern void msgf(
111: 	char type, const char *format, ...);
112: extern int Connect(const char *addr);
113: extern int mkaddr(
114: 	void *addr,
115: 	int *addr_len,
116: 	char *str_addr,
117: 	char *protocol);
118: extern char *BaseName(char *cmd);
119: extern char *strick(char *str);
120: extern int get_tickinfo(TickReq *req, char *addr);
121: extern void broadcast(
122: 	int s, TickReq *quote, struct sockaddr *bc_addr,
123: 	socklen_t bc_len);
124:
125: /* End */
```

您主要感兴趣的条目包括：

-   宏 `DFLT_SERVER`（第 25 行）定义了用于连接报价服务的默认主机名和端口（请注意，非 Yahoo! 的服务器可能会使用不同的电子表格数据格式）。
-   宏 `DFLT_BCAST`（第 30 行）定义了默认的广播地址。默认设置为向回环网络广播，以便那些未安装网卡的读者也能使用。
-   结构体 `Parm`（第 35 至 38 行）定义了一种控制信息解析为 C 数据类型的类型。
-   宏 `TIMEOUT_SECS` 设置为 10 秒，定义了等待股票报价响应的最长时间（第 48 行）。
-   宏 `MAX_TICKERS` 定义了模块 `qserve.c` 中 `tickers[ ]` 的表大小（第 53 行）。
-   结构体 `TickReq`（第 81 至 93 行）为服务器定义了一个股票代码条目。该结构体也用于客户端程序，但结构体成员 `flags` 和 `next_samp` 会被客户端程序忽略。
-   标志 `FLG_UNKNOWN` 和 `FLG_ERROR` 分别定义在第 99 行和第 101 行。

处理完头文件后，请查看列表 18.3，其中展示了 `gettick.c` 源模块。

### 第 18 章：一个实用的网络项目

### 列表 18.3：gettick.c—get_tickinfo() 函数源代码

```c
1: /* gettick.c
2:  *
3:  * Get ticker info from inet:
4:  */
5: #include <quotes.h>
6:
7: /*
8:  * f is set TRUE when a request
9:  * for a stock quote has timed
10:  * out.
11:  */
12: static int f = FALSE;
13:
14: /*
15:  * Catch SIGALRM and Timeout:
16:  */
17: static void
18: sig_ALRM(int signo) {
19:     f = TRUE;    /* Mark timeout */
20: }
21:
22: /*
23:  * Get ticker info:
24:  *
25:  * RETURNS:
26:  *  0       Success
27:  * -1       Failed:
28:  *
29:  * errno:
30:  *  ETIME    Timed Out
31:  *  EBADMSG  Field data format
32:  *  other    Network/system errors.
33:  */
34: int
35: get_tickinfo(TickReq *req, char *addr) {
36:     int z, er;        /* Status, errno */
37:     int s;            /* Socket */
38:     int n;            /* Byte count */
39:     char buff[256];   /* Receive buffer */
40:     char *tkr = NULL; /* Extracted ticker */
41:     struct sigaction
42:                 sa_new,         /* New signal action */
43:                 sa_old;         /* Saved signal action */
44:     Parm  parms[9];     /* Data parse table */
45:
46:     /*
47:      * Initialize parsing parameters. This
48:      * parameter list will need modification
49:      * if yahoo or your quote provider uses
50:      * a different format:
51:      */
52:   parms[0].type = 'S';   /* String */
53:   parms[0].parm = &tkr;    /* Ticker name */
54:   parms[1].type = 'D';   /* Double */
55:   parms[1].parm = &req->last_trade;
56:   parms[2].type = 'S';
57:   parms[2].parm = &req->date;
58:   parms[3].type = 'S';
59:   parms[3].parm = &req->time;
60:   parms[4].type = 'D';
61:   parms[4].parm = &req->change;
62:   parms[5].type = 'D';
63:   parms[5].parm = &req->open_price;
64:   parms[6].type = 'D';
65:   parms[6].parm = &req->high;
66:   parms[7].type = 'D';
67:   parms[7].parm = &req->low;
68:   parms[8].type = 'D';
69:   parms[8].parm = &req->volume;
70:
71:   /*
72:    * Initialize to catch SIGALRM:
73:    */
74:   sa_new.sa_handler = sig_ALRM;
75:   sigemptyset(&sa_new.sa_mask);
76:   sa_new.sa_flags = 0;
77:   sigaction(SIGALRM, &sa_new, &sa_old);
78:
79:   /*
80:    * Connect to finance.yahoo.com:
81:    */
82:   f = FALSE;
83:   alarm(TIMEOUT_SECS);
84:
85:   s = Connect(addr);
86:   if ( s == -1 )
87:        goto errxit;
88:
89:   /*
90:    * Send GET request:
91:    *
92:    * NOTE: This is subject to change.
93:    * If finance.yahoo.com changes, you
94:    * will need to adjust this formatting.
95:    */
96:   sprintf(buf, "GET /d/quotes.csv?"
97:       "s=%s"
98:       "&f=s11dit1c1ohgv"
99:       "&e=.csv\r\n",
100:       req->ticker);
101:
102:   write(s, buf, strlen(buf));
103:   shutdown(s, 1);
104:
105:   /*
106:    * Read response with a timeout:
107:    */
108:   do {
109:       z = read(s, buf, sizeof buf);
110:   } while ( !f && z == -1 && errno == EINTR );
111:
112:   er = errno;
113:   alarm(0);
114:   close(s);
115:
116:   /* Restore the signal action */
117:   sigaction(SIGALRM, &sa_old, NULL);
118:
119:   if ( !f && z > 0 )
120:       n = z;
121:   else {
122:       if ( f )
123:           er = ETIME;
124:       /*
125:        * Report error to log:
126:        */
127:       msgf('e', '%s: Get ticker `%s`: %s',
128:           strerror(er),
129:           req->ticker);
130:
131:       errno = er;
132:       return -1;
133:   }
134:
135:   /* Remove CR, LF, or CRLF */
136:   buf[strcspn(buf, "\r\n")] = 0;
137:
138:   /*
139:    * Check for the unknown ticker case:
140:    */
141:   if ( strstr(buf, "N/A,N/A,N/A,N/A,N/A") ) {
142:       msgf('e', "Unknown Ticker: %s",
143:           req->ticker);
144:       req->flags |= FLG_UNKNOWN;
145:       errno = EBADMSG;       /* For caller */
146:       return -1;             /* Failed */
147:   }
148:
149:   /*
150:    * Parse quote results:
151:    */
152:   if ( (z = extract_params(parms, 9, buf)) < 0 ) {
153:       /* Report failed parse of data */
154:       msgf('e', "Field # %d: '%s': %s", z, buf, ...);
155:       req->flags |= FLG_ERROR;
156:       errno = EBADMSG;       /* For caller */
157:       return -1;             /* Failed */
158:   }
159:
160:   /* Capture the exact case for this ticker */
161:   strncpy(req->ticker, tkr, TICKLEN);
162:   req->ticker[TICKLEN] = 0;
163:
164:   /*
165:    * Update sample time in entry:
166:    */
167:   // req->next_samp = ...;
168:
169:   return 0;
170:
171:   /*
172:    * Error Exit:
173:    */
174: errxit:
175:   alarm(0);
176:   sigaction(SIGALRM, &sa_old, NULL);
177:   return -1;
178: }
```

此模块定义了以下主要组件：

-   第 12 行中的超时标志 `f`。当此标志被设置为 TRUE 时，表示请求已超时。
-   信号捕获函数 `sig_ALRM()`，当计时器过期时会捕获 SIGALRM 信号。此函数在第 19 行将标志变量 `f` 设置为 TRUE。
-   `get_tickinfo()` 函数占据模块的剩余部分，从第 34 行开始。

现在，请查看 `get_tickinfo()` 使用流程：

1.  此函数希望接收的数据是电子表格格式。为了从该格式化记录中解析数据，在数组 `parms` 中建立了一个参数表（第 52 至 69 行）。类型 'S' 表示字符串类型数据，而 'D' 表示要提取的 C 语言双精度浮点数值。
2.  为 SIGALRM 建立信号处理程序（第 74 至 77 行）。
3.  将标志 `f` 初始化为 **FALSE**，并启动计时器（第 82 和 83 行）。
4.  通过调用函数 `Connect()` 并传入报价服务器的地址来发出连接请求（第 85 至 87 行）。`Connect()` 的源代码提供在模块 `connect.c` 中。
5.  格式化 GET 请求（第 96 至 100 行）。如果 Yahoo! 服务器发生变更，这是您可能需要修改的代码区域之一。
6.  将 GET 请求写入报价服务器（第 102 和 103 行）。对 `shutdown(2)` 的调用会向远程服务器发送文件结束通知，而不关闭套接字。这是必要的，以便能够接收来自服务器的响应。
7.  等待并读取生成的电子表格记录（第 108 至 110 行）。
8.  如果发生错误，将 `errno` 的值保存在变量 `er` 中（第 112 行）。
9.  取消计时器（第 113 行）并关闭套接字 `s`（第 114 行）。
10. 恢复信号 SIGALRM 的信号处理程序（第 117 行）。
11. 如果标志 `f` 仍为 **FALSE** 且 `z` 大于零，则程序成功接收到一些报价数据（第 119 和 120 行）。接收的字节数记录在变量 `n` 中。
12. 否则，如果 `f` 为 **TRUE**，则将在 `er` 中保存的错误值设置为 **ETIME**，以指示发生了超时（第 123 行）。
13. 第 127 至 132 行处理报价未成功接收时的超时或错误情况。对 `msgf()` 的调用会将错误消息记录到 syslog 日志设施中。
14. 从接收到的电子表格记录中移除回车符或换行符（第 136 行）。
15. 测试一个特定序列，该序列表示股票代码未知（第 141 至 147 行）。如果股票代码未知，Yahoo! 会对多个字段返回 **N/A**。
