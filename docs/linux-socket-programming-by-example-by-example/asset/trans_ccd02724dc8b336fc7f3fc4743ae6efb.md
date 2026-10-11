
## 第 10 章：在套接字上使用标准 I/O

### 列表 10.5：续

```c
355: char *oper;
356: rpn_spec func;
357: } spec[] = {
358: { "dup", rpn_dup },
359: { "swap", rpn_swap },
360: { "seed", rpn_seed },
361: { "random", rpn_random },
362: { "tprime", rpn_test_prime },
363: { "genprime", rpn_genprime },
364: { 0 }
365: };
366: static struct {
367: char *oper;
368: mpz_func func;
369: } binops[] = {
370: { "+", mpz_add },
371: { "-", mpz_sub },
372: { "*", mpz_mul },
373: { "/", mpz_tdiv_q },
374: { "%", mpz_tdiv_r },
375: { "gcd", mpz_gcd },
376: { 0 }
377: };
378: static struct {
379: char *oper;
380: mpz_unary func;
381: } unary[] = {
382: { "abs", mpz_abs },
383: { "neg", mpz_neg },
384: { "sqrt", mpz_sqrt },
385: { 0 }
386: };

387: /*
388: * 特殊情况：
389: */
390: for ( x=0; spec[x].oper; ++x )
391: if ( !strcmp(spec[x].oper,oper) )
392: return spec[x].func();

393: /*
394: * 测试是否匹配二元运算符：
395: */
396: for ( x=0; binops[x].oper; ++x )
397: if ( !strcmp(binops[x].oper,oper) )
398: return rpn_binoper(binops[x].func);

399:
400: /*
401: * 测试是否匹配一元运算符：
402: */
403: for ( x=0; unary[x].oper; ++x )
404: if ( !strcmp(unary[x].oper,oper) )
405: return rpn_unaryop(unary[x].func);

406: return -1; /* 失败：未知运算符 */
407: }

408:
409: void
410: rpn_process(FILE *tx,char *buf) {
411: int z;
412: mpz_t *t;
413: char *operation;
414: char *operand;

415: operation=strtok(buf,";\n\r");
416: operand=strtok(NULL,";\n\r");

417: if ( !strcmp(operation,"dump") ) {
418: rpn_dump(tx);

419: } else if ( !strcmp(operation,"=") ) {
420: /*
421: * 弹出结果：
422: */
423: if ( ( z = rpn_pop(&t) ) == -1 )
424: fputs("E:Nothing to pop\n",tx);
425: else {
426: fprintf(tx,"%d:\"",z);
427: mpz_out_str(tx,10,*t);
428: fputc('\'', tx);
429: rpn_free(&t);
430: }

431: } else if ( !strcmp(operation,"#") ) {
432: /*
433: * 将操作数压入栈中：
434: */
435: t = rpn_alloc();
436: if ( !mpz_set_str(*t,operand,10) )
437: fprintf(tx,"%d:\n",rpn_push(t));
438: else {
439: fputs("E:Invalid number\n",tx);
440: rpn_free(&t);
441: }
442: } else {
443: /*
444: * 执行操作：
445: */
446: z = rpn_opr(operation);
447: if ( z == -1 )
448: fprintf(tx,
449: "E:Operation failed.\n");
450: else
451: fprintf(tx,"%d:\n",z);
452: }
453: fflush(tx);
454: }
```

尽管列表 10.5 相当长，但其中只有服务器概念对你重要。因此，只描述 `rpn_process()` 函数：

1.  调用 `rpn_process()` 函数时，传入用于写入的输出流（参数 tx）和要处理的输入文本行 buf（第 413 行）。
2.  变量 `operation` 和 `operand` 分别是解析后的操作符和操作数字符串（第 419 至 420 行）。
3.  如果操作是特殊操作 "dump"，则调用函数 `rpn_dump()` 来列出栈的内容（第 422 至 423 行）。
4.  如果第 3 步不适用，且操作是 "="，则值从栈中弹出并返回给客户端程序（第 425 至 436 行）。继续执行第 7 步。
5.  如果第 3 步和第 4 步都不适用，且操作是 "#"，则操作数值被压入栈中（第 438 至 448 行）。继续执行第 7 步。
6.  如果第 3、4、5 步都不适用，所有其他 RPN 操作都由函数 `rpn_opr()` 处理。报告给客户端的结果是栈索引值或错误指示（第 454 至 460 行）。
7.  通过在第 462 行调用 `fflush(tx)`，强制将输出写入套接字。

服务器在客户端一侧的工作方式，将在展示完服务器代码的其余部分后进行考察。列表 10.6 显示了服务器源代码的剩余部分。这代表了服务器的主要程序段。

### 列表 10.6：rpnsvr.c —— RPN 主服务器代码

![](img/961a0296fe36074690a9847b79332eff_277_0.png)

```c
1: /* rpnsvr.c;
2:  *
3:  * 示例 RPN 服务器：
4:  */
5: #include <stdio.h>
6: #include <unistd.h>
7: #include <stdlib.h>
8: #include <errno.h>
9: #include <string.h>
10: #include <time.h>
11: #include <sys/types.h>
12: #include <sys/socket.h>
13: #include <netinet/in.h>
14: #include <arpa/inet.h>
15: #include <netdb.h>
16:
17: #ifndef SHUT_RDWR
18: #define SHUT_RDWR 3
19: #endif
20:
21: extern int maddr(void *addr,
22: 	int *addr_len,
23: 	char *input_address,
24: 	char *protocol);
25:
26: extern void rpn_process(FILE *tx,
27: 	char *buf);
28:
29:
30: /*
31:  * 此函数报告错误并
32:  * 返回到 shell：
33:  */
34: static void
35: bail(const char *on_what) {
36: 	if ( errno != 0 ) {
37: 		fputs(strerror(errno),stderr);
38: 		fputs(": ",stderr);
39: 	}
40: 	fputs(on_what,stderr);
41: 	fputs('\n',stderr);
42: 	exit(1);
43: }
44:
45: int
46: main(int argc,char **argv) {
47: int z;
48: char *srvr_addr = "127.0.0.1:9090";
49: struct sockaddr_in addr_srvr;/* AF_INET */
50: struct sockaddr_in addr_clnt;/* AF_INET */
51: int len_inet;             /* 长度 */
52: int s = -1;               /* 套接字 */
53: int c = -1;               /* 客户端套接字 */
54: FILE *rx = NULL;          /* 读流 */
55: FILE *tx = NULL;          /* 写流 */
56: char buf[4096];           /* I/O 缓冲区 */
57:
58: /*
59:  * 使用来自命令行
60:  * 的服务器地址，否则默认为 127.0.0.1：
61: */
62: if ( argc >= 2 )
63: srvr_addr = argv[1];
64:
65: len_inet = sizeof addr_srvr;
66: z = mkaddr(&addr_srvr,&len_inet,
67: srvr_addr,"tcp");
68:
69: if ( z < 0 || !addr_srvr.sin_port ) {
70: fprintf(stderr,"Invalid server \
71: address, or no port number \
72: was specified.\n");
73: exit(1);
74: }
75:
76: /*
77:  * 创建一个 TCP/IP 套接字以使用：
78: */
79: s = socket(PF_INET,SOCK_STREAM,0);
80: if ( s == -1 )
81: bail("socket(2)");
82:
83: /*
84:  * 绑定服务器地址：
85: */
86: z = bind(s,(struct sockaddr *)&addr_srvr,
87: len_inet);
88: if ( z == -1 )
89: bail("bind(2)");
90:
91: /*
92:  * 使其成为监听套接字：
93: */
94: z = listen(s,10);
95: if ( z == -1 )
96: bail("listen(2)");
97:
98: /*
99: * 启动服务器循环：
100: */
101: for (;;) {
102: /*
103: * 等待连接：
104: */
105: len_inet = sizeof adr_clnt;
106: c = accept(s,
107: (struct sockaddr *)&adr_clnt,
108: &len_inet);
109: if ( c == -1 )
110: bail("accept(2)");
111:
112: /*
113: * 创建流：
114: */
115: rx = fdopen(c,"r");
116: if ( !rx ) {
117: /* 失败 */
118: close(c);
119: continue;
120: }
121:
122: tx = fdopen(dup(c),"w");
123: if ( !tx ) {
124: fclose(rx);
125: continue;
126: }
127:
128: /*
129: * 将两个流都设置为按行
130: * 缓冲模式：
131: */
132: setlinebuf(rx);
133: setlinebuf(tx);
134:
135: /*
136: * 处理客户端请求：
137: */
138: while ( fgets(buf,sizeof buf,rx) )
139: rpn_process(tx,buf);
140:
141: /*
142: * 关闭此客户端的连接：
143: */
144: fclose(tx);
145: shutdown(fileno(rx),SHUT_RDWR);
146: fclose(rx);
147: }
148:
149: /* 控制永远不会到达这里 */
150: return 0;
151: }
```

列表 10.6 中服务器代码的主要特性你现在应该相对熟悉了。此模块使用的基本步骤如下：

1.  C 宏 `SHUT_RDWR` 在第 18 行定义，如果该宏尚未定义。这使得在程序后部调用 `shutdown(2)` 时源代码更清晰。
2.  如果存在，则从命令行获取服务器地址（第 62 和 63 行）。
3.  在第 65 至 74 行中调用 `mkaddr()` 子例程为我们构建服务器地址。
4.  创建服务器套接字（第 79 至 81 行）。
5.  将服务器地址绑定到套接字（第 86 至 89 行）。
6.  将套接字变为监听套接字（第 94 至 96 行）。
7.  程序等待客户端连接（第 105 至 110 行）。
8.  在第 115 至 126 行中创建输入和输出文件流。注意错误恢复必须确保当前打开的流和客户端套接字被关闭。如果发生错误，此服务器不会报告该错误本身。
9.  将 I/O 流设置为按行缓冲模式（第 132 至 133 行）。
10. 在达到 EOF 之前，从客户端读取每个文本行并由函数 `rpn_process()` 处理（第 138 至 139 行）。
11. 为此客户端执行完全关闭（第 144 至 146 行）。
12. 重复第 7 步以容纳下一个客户端连接。

