

另一种该问题的表现形式是在调用 `fork(2)` 函数之后。任何在 `fork` 操作之前存在的套接字都会被复制到子进程中。

> **提示**
>
> 每当需要立即或部分关闭操作时，请始终使用 `shutdown(2)` 函数，而不是 `close(2)` 函数。来自 `dup(2)`、`dup2(2)` 或 `fork(2)` 操作的重复文件描述符可能会阻止 `close(2)` 函数发起任何关闭操作，直到最后一个未处理的描述符被关闭为止。

## 关闭套接字的读取端

关闭套接字的读取端会导致任何待处理的读取数据被静默忽略。如果从远程套接字发送了更多数据，这些数据同样会被静默忽略。然而，进程尝试从该套接字读取时，将返回一个错误。这通常用于强制协议或帮助调试代码。

## 何时不使用 `shutdown(2)`

`shutdown(2)` 函数的文档中列出了表 1.2 所示的错误。

*表 1.2：`shutdown(2)` 可能返回的错误*

| 错误 | 描述 |
| :--- | :--- |
| EBADF | 给定的套接字不是有效的文件描述符。 |
| ENOTSOCK | 给定的文件描述符不是套接字。 |
| ENOTCONN | 指定的套接字未连接。 |

从表 1.2 可以看出，您只应对已连接的套接字调用 `shutdown(2)`。否则，将返回错误代码 `ENOTCONN`。

> **注意**
>
> 即使使用 `SHUT_RDWR`，`shutdown(2)` 函数也不会释放套接字的文件单元号。套接字的文件描述符保持有效并处于使用状态，直到调用 `close(2)` 函数将其释放。
>
> 还需注意，只要套接字仍处于连接状态，`shutdown(2)` 可以针对同一个文件单元多次调用。

## 编写一个客户端/服务器示例

现在，您已经查看了足够的套接字 API 集合，可以开始享受其中的乐趣了。在本节中，您将以一对套接字进行通信，审查、编译并测试一个简单的客户端和服务器进程。

为了将编程代码降到最低限度，一个程序启动后将分叉为客户端进程和服务器进程。子进程将承担客户端进程的角色，而原始父进程将执行服务器的角色。图 1.3 说明了父子进程以及将使用的套接字之间的关系。

![](img/961a0296fe36074690a9847b79332eff_42_0.png)

**图 1.3**：使用 fork(2) 和 socketpair(2) 的客户端/服务器示例。

父进程是原始启动进程。它将立即通过调用 socketpair(2) 请求一对套接字，然后通过调用 fork(2) 将自己分叉为两个进程。

服务器将接受一个请求，对该请求进行处理，然后退出。在此示例中，客户端同样将发出一个请求，报告服务器响应，然后退出。

请求将是 strftime(3) 函数的第三个参数的形式。这是一个格式字符串，用于格式化日期和时间字符串。服务器将在接收到请求时获取当前的日期和时间。服务器将使用客户端的请求字符串将其格式化为最终字符串，并将其返回给客户端。作为回顾，strftime(3) 函数的原型如下：

```c
#include <time.h>
```

![](img/961a0296fe36074690a9847b79332eff_42_1.png)

```c
size_t strftime(char *buf,
size_t max,
const char *format,
const struct tm *tm);
```

参数 `buf` 和 `max` 分别指示输出缓冲区及其最大长度。参数 `format` 是一个输入字符串，允许您格式化日期和时间字符串（清单 1.3 第 75 行展示了这样一个字符串的示例）。最后，参数 `tm` 用于提供创建输出日期和时间字符串所需的所有日期和时间组件。如有需要，请查阅 strftime(3) 的手册页。

清单 1.3 展示了演示客户端/服务器程序的源代码列表。

### 清单 1.3：$ 01lst03.c——使用 socketpair(2) 和 fork(2) 的客户端/服务器示例

```c
  1:  /*  清单 1.3
  2:    *
  3:    * 使用 socketpair(2)
  4:    * 和 fork(2) 的客户端/服务器示例：
  5:    */
  6:
  7:  #include <stdio.h>
  8:  #include <stdlib.h>
  9:  #include <unistd.h>
 10:  #include <errno.h>
 11:  #include <string.h>
 12:  #include <time.h>
 13:  #include <sys/types.h>
 14:  #include <sys/socket.h>
 15:  #include <sys/wait.h>
 16:
 17:  /*
 18:    *
 19:    * 截至 RedHat-6.0，这些仍未定义：
 20:    */
 21:  #ifndef SHUT_RD
 22:  #define SHUT_RD      0
 23:  #define SHUT_WR      1
 24:  #define SHUT_RDWR    2
 25:  #endif
 26:
 27:  /*
 28:    * 主程序：
 29:    */
 30:  int
 31:  main(int argc,char **argv) {
 32:      int z;            /*  状态返回码 */
 33:      int s[2];        /*  套接字对   */
 34:      char *msgp;     /*  消息指针 */
 35:      int mlen;        /*  消息长度    */
 36:      char buf[80];    /*  工作缓冲区       */
 37:      pid_t child;     /*  子进程 PID */
 38:
 39:      /*
 40:        * 创建一对本地套接字：
 41:        */
 42:      z = socketpair(AF_LOCAL,SOCK_STREAM,0,s);
 43:      if (z == -1) {
 44:          fprintf(stderr,"$s: socketpair(2)\n",
 45:                  strerror(errno));
 46:          exit(1);
 47:      }
 48:      /*
 49:       * 现在 fork() 分叉为两个进程：
 50:       */
 51:      if ((child = fork()) == pid_t -1) {
 52:          /*
 53:           * 分叉为两个进程失败：
 54:           */
 55:          fprintf(stderr,"%s: fork(2)\n",
 56:                  strerror(errno));
 57:          exit(1);
 58:      } else if (child == 0) {
 59:          /*
 60:           * 这是子进程（客户端）：
 61:           */
 62:          char rxbuf[80]; /* 接收缓冲区 */
 63:          printf("Parent PID is %ld\n",(long)getppid());
 64:          close(s[0]);      /* 服务器使用 s[1] */
 65:          s[0] = -1;        /* 忘记此单元 */
 66:          /*
 67:           * 形成消息及其长度：
 68:           */
 69:          msgp = "%A %d-%b-%Y %l:%M %p";
 70:          mlen = strlen(msgp);
 71:          printf("Child sending request '%s'\n",msgp);
 72:          fflush(stdout);
 73:          /*
 74:           * 向服务器写入请求：
 75:           */
 76:          z = write(s[1],msgp,mlen);
 77:          if (z < 0 ) {
 78:              fprintf(stderr,"%s: write(2)\n",
 79:                  strerror(errno));
 80:              exit(1);
 81:          }
 82:          /*
 83:           * 现在指示我们不会再向我们的套接字写入
 84:           * 任何内容，通过关闭套接字的写入端：
 85:           */
 87:          if ( shutdown(s[1],SHUT_WR) == -1 ) {
 88:              fprintf(stderr,"%s: shutdown(2)\n",
 89:                  strerror(errno));
 90:              exit(1);
 91:          }
 92:
 93:          /*
 94:           * 接收来自服务器的回复：
 95:           */
 96:          z = read(s[1],rxbuf,sizeof rxbuf);
 97:          if ( z < 0 ) {
 98:              fprintf(stderr,"%s: read(2)\n",
 99:                  strerror(errno));
100:              exit(1);
101:          }
102:
103:          /*
104:           * 在我们从服务器
105:           * 接收的数据末尾添加一个空字节：
106:           */
107:          rxbuf[z] = 0;
108:
109:          /*
110:           * 报告结果：
111:           */
112:          printf("Server returned '%s'\n",rxbuf);
113:          fflush(stdout);
114:
115:          close(s[1]);	/* 现在关闭我们这一端 */
116:
117:      } else {
118:
119:          /*
120:           * 这是父进程（服务器）：
121:           */
122:          int status; /* 子进程终止状态 */
123:          char txbuf[80];		/* 回复缓冲区 */
124:          time_t td;    /* 当前日期和时间 */
125:
126:          printf("Child PID is %ld\n", (long)child);
127:          fflush(stdout);
128:
129:          close(s[1]);   /* 客户端使用 s[1] */
130:          s[1] = -1;     /* 忘记此描述符 */
131:
132:          /*
133:             * 等待来自客户端的请求：
134:             */
135:          z = read(s[0], buf, sizeof buf);
136:
137:          if ( z < 0 ) {
138:                fprintf(stderr, "%s: read(2)\n",
139:                        strerror(errno));
140:                exit(1);
141:          }
142:
143:          /*
144:             * 在我们从客户端
145:             * 接收的消息末尾添加一个空字节：
146:             */
147:          buf[z] = 0;
148:
149:          /*
150:             * 现在对接收到的消息
151:             * 执行服务器功能：
152:             */
153:          time(&td);      /* 获取当前时间 */
154:
155:          strftime(txbuf, sizeof txbuf,  /* 缓冲区 */
156:                   buf,               /* 输入格式 */
157:                   localtime(&td));   /* 输入时间 */
158:
159:          /*
160:             * 将响应发送回客户端：
161:             */
162:          z = write(s[0], txbuf, strlen(txbuf));
163:
164:          if ( z < 0 ) {
165:                fprintf(stderr, "%s: write(2)\n",
166:                        strerror(errno));
167:                exit(1);
168:          }
169:
170:          /*
```

