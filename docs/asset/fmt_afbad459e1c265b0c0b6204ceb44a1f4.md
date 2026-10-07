
为了获取设备的设置，你必须打开设备并在 `tcgetattr()` 调用中使用文件描述符。这对于许多设备来说是一个问题，这些设备通常只能打开一次以防止设备竞争。幸运的是，给 `open()` 传递 `O_NONBLOCK` 标志会使其立即打开且不在任何操作上阻塞。然而，你可能仍然希望在 `read` 上阻塞；如果是这样，在读写之前，使用 `fcntl()` 关闭 `O_NONBLOCK`：

```c
fcntl(fd, F_SETFL, fcntl(fd, F_GETFL) & ~O_NONBLOCK);
```

`term` 标志控制管理输入输出的四个部分。输入标志 `c_iflag` 决定接收到的字符如何被解释和处理。输出标志 `c_oflag` 决定你向终端写入的字符如何被解释和处理。控制标志 `c_cflag` 决定设备的串口协议特性，对物理设备有用。本地标志 `c_lflag` 决定字符在发送到输出之前如何被收集和处理。

# 第 15 章 终端与伪终端

![](img/03c623925f5ce79517eccfa53893f339_299_0.png)

图 15.1 显示了这些标志如何融入字符处理的宏大蓝图中的简化视图。

我们将首先演示使用 `termios` 的方法，然后提供其简短参考资料。

## 15.3 termios 示例

### 15.3.1 密码

修改 `termios` 设置的一个常见原因是在不回显字符的情况下读取密码。为了这一点，你需要在读取密码时关闭本地回显（local echo）。你的代码看起来如下：

```c
struct termios ts, ots;
```

一个结构体保留原始的 `termios` 设置以便你恢复它们，另一个是用于修改的副本。

```c
tcsetattr(STDIN_FILENO, &ts);
```

通常，你将从标准输入读取密码。

```c
ots = ts;
```

保留一份原始 `termios` 设置的副本以便稍后恢复。

```c
ts.c_lflag &= ~ECHO;
ts.c_lflag |= ECHONL;
tcsetattr(STDIN_FILENO, TCSAFLUSH, &ts);
```

在所有当前待处理输出完成后，关闭换行符以外的字符回显。`c_lflag` 中的第一个 `l` 代表本地处理（local processing）。

```c
read_password();
```

在这里，你读取密码。这可能只是简单的单个 `fgets()` 或 `read()` 调用，也可能包含更复杂的处理，取决于 tty 处于原始模式（raw mode）还是熟火模式（cooked mode），取决于你程序的需求。

```c
tcsetattr(STDIN_FILENO, TCSANOW, &ts);
```

这会恢复原始的 `termios` 设置并立即生效：我们将在第 290 页的参考部分解释其他选项。）

一个完整的示例程序 `readpass` 如下：

```c
1: /* readpass - 在不回显的情况下读取密码 *
2: #include <stdio.h>
3: #include <termios.h>
4: #include <unistd.h>
5:
6: int main(void) {
7:   struct termios ts, ots;
8:   char passbuf[1024];
9:
10:  /* 获取并保存当前的 termios 设置 */
11: tcgetattr(STDIN_FILENO, &ts);
12: ots = ts;
13:
14:  /* 更改并设置新的 termios 设置 *
15: ts.c_lflag &= ~ECHO;
16: ts.c_lflag |= ECHONL;
17: tcsetattr(STDIN_FILENO, TCSAFLUSH, &ts);
18:
19:  /* 谨慎起见：检查设置是否生效 */
20: tcgetattr(STDIN_FILENO, &ts);
21: if (ts.c_lflag & ECHO) {
22:     fprintf(stderr, "Failed to turn off echo\n");
23:     tcsetattr(STDIN_FILENO, TCSANOW, &ts);
24: }
25:
26:
27:  /* 获取并打印密码 */
28: printf("enter password: %s");
29: fflush(stdout);
30: getpass(passbuf, 1024, stdin);
31: printf("read password: %s", passbuf);
32: } /* passbuf 中有一个终端符 \n */
33:
34:  /* 恢复旧的 termios 设置 */
35: tcsetattr(STDIN_FILENO, TCSANOW, &ts);
36:
37: exit(0);
38: )
```

### 15.3.2 串口通信

作为一个对 tty 两端进行编程的示例，这里有一个将当前终端连接到串口的程序。在一个 tty 上，名为 `robin` 的程序会在你打字时与你交流。在另一个 tty 上，它正在与串口通信。为了对本地 tty 和串口的输入和输出进行多路复用，该程序使用了第 209 页描述的 `select()` 系统调用。

以下是完整的 `robin.c` 及其后的解释。

```c
1: /* robin.c -- 实现简单的串口端口交互程序 */
2: #include <sys/time.h>
3: #include <sys/types.h>
4: #include <errno.h>
5: #include <fcntl.h>
6: #include <popt.h>
7: #include <stdio.h>
8: #include <stdlib.h>
9: #include <signal.h>
10: #include <string.h>               /* 用于 strerror() */
11: #include <termios.h>
12: #include <unistd.h>
13:
14: void usage(int exitcode, char *error, char *addl) {
15:     printf(stderr, "Usage: robin [options] <port>\n\n
16:       "[options] include:\n
17:       "-H 用于帮助
18:       "-r 用于原始模式
19:       "-c 在输出时添加 CR
20:       "-h 用于硬件流控
21:       "-s 用于软件流控
22:       "-n 用于无流控
23:       "-b <bps> 指定波率);\n"
24:     if (error) printf(stderr, ":%s: %s\n", error, addl);
25:     exit(exitcode);
26: }
27:
28: speed_t symbolic_speed(int speed) {
29:     if (speed >= 460800) return B460800;
30:     if (speed >= 230400) return B230400;
31:     if (speed >= 115200) return B115200;
32:     if (speed >= 57600) return B57600;
33:     if (speed >= 38400) return B38400;
34:     if (speed >= 19200) return B19200;
35:     if (speed >= 9600) return B9600;
36:     if (speed >= 4800) return B4800;
37:     if (speed >= 2400) return B2400;
38:     if (speed >= 1800) return B1800;
39:     if (speed >= 1200) return B1200;
40:     if (speed >= 600) return B600;
41:     if (speed >= 300) return B300;
42:     if (speed >= 200) return B200;
43:     if (speed >= 150) return B150;
44:     if (speed >= 134) return B134;
45:     if (speed >= 110) return B110;
46:     if (speed >= 75) return B75;
47:     return B50;
48: )
49:
50: /* 这些需要文件作用域，以便在
51: * 信号处理器中使用 */
52: /* 用于恢复的端口 termios 设置 */
53: static termios pots;
54: /* 用于恢复的 stdout/in termios 设置 */
55: static termios sots;
56: /* 端口描述符 */
57: int pf;
58:
59: /* 退出时恢复终端设置 */
60: void cleanup_termios(int signal) {
61:     tcsetattr(pf, TCSANOW, &pots);
62:     tcsetattr(STDIN_FILENO, TCSANOW, &sots);
63:     exit(0);
64: }
65:
66: /* 处理单个转义字符 */
67: void send_escape(int fd, char c) {
68:     switch (c) {
69:             /* 恢复 termios 设置并退出 */
70:             cleanup_termios(0);
71:             break;
72:             case 'b':
73:                 /* 发送中断 */
74:                 tcsendbreak(fd, 0);
75:                 break;
76:             default:
77:                 /* 通过字符 */
78:                 /* "C-" 发送 "C-" */
79:                 write(fd, &c, 1);
80:                 break;
81:     }
82:
83:     return;
84: }
85:
86: /* * 处理转义字符，写入输出 */
87: void cook_buf(int fd, char *buf, int num) {
88:     int current = 0;
89:     static int in_escape = 0;
90:
91:     if (in_escape) {
92:         /* cook_buf 带不完整的转义序列被调用 */
93:         send_escape(fd, buf[0]);
94:         num--;
95:         buf++;
96:         in_escape = 0;
97:     }
98:     while (current < num) {
99:         # define CTRLCHAR(c) ((c)-0x40)
100:        while (current < num) && buf[current] != CTRLCHAR('\\')) current++;
101:        if (current) write(fd, buf, current);
102:        if (current < num) {
103:            /* 找到转义字符 */
104:            current++;
105:            in_escape = 1;
106:            send_escape(fd, buf[current]);
107:            num--;
108:            buf++;
109:            current = 0;
110:        }
111:    }
112:    return;
113: }
114: int main(int argc, char *argv[]) {
115:    char c;
116:    int speed = 0;
117:    int raw = 0;
118:    int i = 0;
119:    int done = 0;
120:    #define BUFSIZE 1024
121:    char buf(BUFSIZE);
122:    poptopt optCont;
123:    struct poptOption optionTable[] = {
124:        { "bps", 'b', POPT_ARG_INT,&speed, 0 },
125:        { "crni", 'c', 0, 0, 'c' },
126:        { "help", 'H', 0, 0, 'H' },
127:        { "hwflow", 'h', 0, 0, 'h' },
128:        { "nflow", 'n', 0, 0, 0 },
129:        { "raw", 'r', 0, &raw, 0 },
130:        { "swflow", 's', 0, 0, 's' },
131:        { NULL, 0, NULL, 0 }, };
132:    };
133:
134:    #ifndef SLEEP
135:        /* 等待 10 分钟以便附加调试器 */
136:        sleep(600);
137:    #endif
138:
139:    if (argc < 2) usage(1, "Not enough arguments", "\n");
140:
141:    /* 通常情况下，我们会让 popt 确定哪个参数是
142:    端口名。在这里我们强制让它是最后一个，这
143:    简化了剩余的选项解析。 */
144:    portname = argv[argc - 1];
145:    pf = open(portname, O_RDWR);
146:    if (pf < 0)
147:        usage(1, strerror(errno), portname);
148:
149:    /* 修改端口配置 */
150:    tcgetattr(pf,&pts);
151:    pots = pts;
152:    /*一些我们想要任意设置的内容 */
153:    pts.c_lflag &= ~ICANON;
154:    pts.c_lflag &= ~(ECHO | ECHONL);
```
