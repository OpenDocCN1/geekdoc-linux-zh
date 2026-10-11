
```c
1: /* robin.c -- 实现简单的串口交互程序 */
2: #include <sys/time.h>
3: #include <sys/errno.h>
4: #include <errno.h>
5: #include <fcntl.h>
6: #include <popt.h>
7: #include <stdio.h>
8: #include <stdlib.h>
9: #include <signal.h>
10: #include <string.h> /* 用于 strerror() */
11: #include <termios.h>
12: #include <unistd.h>
13:
14: void usage(int exitcode, char *error, char *addl) {
15: fprintf(stderr, "Usage: robin [options] <port>\n"
16:     "[options] include: \n"
17:     "-H 显示此帮助\n"
18:     "-r 进入原始模式(raw mode)\n"
19:     "-c 在输出时添加带 NL 的 CR\n"
20:     "-h 硬件流控制\n"
21:     "-s 软件流控制\n"
22:     "-n 无流控制\n"
23:     "-b <bps> 设置波特\n");
24: if (error) fprintf(stderr, "%s: %s\n", error, addl);
25: exit(exitcode);
26: }
27:
28: speed_t symbolic_speed(int speed) {
29: if (speed >= 460800) return B460800;
30: if (speed >= 230400) return B230400;
31: if (speed >= 115200) return B115200;
32: if (speed >= 57600) return B57600;
33: if (speed >= 38400) return B38400;
34: if (speed >= 19200) return B19200;
35: if (speed >= 9600) return B9600;
36: if (speed >= 4800) return B4800;
37: if (speed >= 2400) return B2400;
38: if (speed >= 1800) return B1800;
39: if (speed >= 1200) return B1200;
40: if (speed >= 600) return B600;
41: if (speed >= 300) return B300;
42:   if (speed >= 200) return B200;
43:   if (speed >= 150) return B150;
44:   if (speed >= 134) return B134;
45:   if (speed >= 110) return B110;
46:   if (speed >= 75) return B75;
47:     return B850;
48: 
49:   /* 这些需要具有文件作用域，以便在信号处理程序中使用它们 */
50:   /* 恢复串口的 termios 设置 */
51:   struct termios pots;
52:   /* 恢复 stdout/in 的 termios 设置 */
53:   struct termios sots;
54:   /* 端口描述符 */
55:   int;
56: 
57:   /* 退出时恢复 termios 设置 */
58:   void cleanup_termios(int signal) {
59:     tcsetattr(fd, TCSANOW, &pots);
60:     tcsetattr(STDIN_FILENO, TCSANOW, &sots);
61:     exit(0);
62: }
63: 
64:   /* 处理单个字符 */
65:   void send_escape(int fd, char c) {
66:     switch (c) {
67:       case 'q':
68:         /* 恢复 termios 设置并退出 */
69:         cleanup_termios();
70:         break;
71:       case 'b':
72:         /* 发送 break */
73:         tbreak(fd, 0);
74:         break;
75:       default:
76:           /* 透传字符 */
77:           write(fd, &c, 1);
78:         break;
79:   }
80:   return;
81: 
82:   /* 处理写入输出的转义字符 */
83:   void cook_buf(int fd, char *buf, int num) {
84:     int current = 0;
85:     static int in_escape = 0;
86: 
87:     if (in_escape) {
88:         /* 以不完整的转义序列时调用 cook_buf */
89:         send_escape(fd, buf[0]);
90:         num--;
91:         buf++;
92:         in_escape = 0;
93:     }
94:     #define CTRLCHAR '\0'
95:     while (current < num && (buf[current] != CTRLCHAR)) current++;
96:     write(fd, buf, current);
97:     if (current < num) {
98:         /* 查找转义字符 */
99:         current++;
100:        if (current >= num) {
101:            /* 解释序列的第一个字符 */
102:            in_escape = 1;
103:            return;
104:        }
105:        send_escape(fd, buf[current]);
106:        num = current;
107:        buf += current;
108:        current = 0;
109:    }
110:    return;
111: }
112:: int(int11111[])1 { { {


111:     struct termios *ptmios; /* 端口的 termios 设置 */
114:     struct termios sts; /* stdout/in的 termios 设置 */
115: */char *portname;
116: */
117:     int speed = 0;      /* 用于在参数解析中设置速度 */
118:    struct sigaction act/* 用于初始化信号处理程序 */
119:    fd_set ready;       /* 用于 select */
120:    int raw = 0;        /* 原始模式？ */
121:    int i = 0;          /* 用于多路复用循环 */
122:    int done = 0;      
123:    #define BUFFSIZE 1024
124:    char buf[BUFFSIZE];
125:    poptopt context opt; /* 解析命令行选项的上下文 */
126:    struct poptoptoptionTable[] = {
127:        {"bps", "b", "POPT_ARG_INT", &speed, 0},
128:        {"crml", "c", 0, "c"},
129:        {"neip", "H", 0, 0, "H"},
130:        {"hwflow", "h", 0, 0, "h"},
131:        {"raw", "r", 0, &raw, 0},
132:        {"swflow", "s", 0, 0, "s"},
133:
134:        {NULL, 0, NULL, 0}
135:    };
136: 
137:    #ifdef DSLEEP
138:        /* 等待10分钟 */
139:        sleep(60);
140:    #endif
141:    if (argc < 2) {
142:        usage(1, "Not enough arguments", "");
143:    }
144:    /* 通常情况下，我们处理剩余的参数解析。 */
145:    portname = argv[argc-1];
146:    pf = open(portname, O_RDWR);
147:    if (pf < 0) {
148:        usage(1, strerror(errno), portname);
149:    }
150:    /* 修改端口配置 */
151:    tcgetattr(pf, &pts);
152:    pts -= pts;
153:    /* 我们想要设置的内容 */
154:    pts.c_lflag &= -ICAN;
155:    pts.c_lflag &= ~(ECHO | ECHON);
156: 
157:    /* 现在处理本地终端侧 */
158:    tcgetattr(STDIN_FILENO, &sts);
159:    sots = sts;
160:    /* 再次，一些任意设置 */
161:    pts.c_iflag &= ~BRKINT;
162:    pts.c_iflag |= IBRON;
163:    pts.c_iflag &= ~ISIG;
164:    pts.c_cc[VMIN] = 1;
165:    pts.c_cc[VTIME] = 0;
166:    pts.c_iflag &= ~ICANON;
167:    /* 本地回显：允许另一端进行回显 */
168:    pts.c_iflag &= ~(ECHO | ECHONL);
169: 
170:    optCon = popgetContext("robin", argc, argv, optionsTable, 0);
171: 
172:    /* 选项处理现在将修改 pts 和 sts */
173:    while ((c = popgetNextOpt(optCon)) >= 0) {
174:      switch (c) {
175:        case 'H':
176:            usage(0, NULL, NULL);
177:          break;
178:      case 'c':
179:            /* 发送带 NL 的 CR */
180:            pts.c_oflag |= ONLCR;
181:            break;
182:      case 'h':
183:            /* 硬件流控制 */
184:            pts.c_cflag |= CRTSCTS;
185:            pts.c_iflag &= ~(IXON | IXSOFF | IXANY);
186:            break;
187:      }
188:    }
189: }
```
