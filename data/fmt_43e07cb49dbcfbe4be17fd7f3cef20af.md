
该文件包含了所有标志定义。`c_iflag`处理所有输入，这意味着从设备发送的字符在读取之前会被处理。同样，`c_oflag`包含了端口设置，如波特率、位、停止位等。本地标志`c_cflag`决定是否回显。默认值定义在`<asm/termbits.h>`中。标志在手册 (2) 中描述。

## 2.3 串口设备的输入概念

这里将介绍三种不同的输入概念。必须根据应用选择合适的概念。尽量不要循环读取单个字符来获取完整字符串。当我这样做时，会丢失字符，而读取整个字符串则没有出现错误。

### 2.3.1 规范输入处理

这是终端的正常处理模式，对于与其他设备通信也很有用。输入是以行为单位处理的，这意味着读取将返回一整行。行默认由`NL`（`ASCII LF`）、文件结束或换行符终止。`CR`（`DOS/Windows`换行）不会终止行。规范输入处理还可以处理删除、删除单词和打印字符。

### 2.3.2 非规范输入处理

非规范输入处理每次读取处理固定数量的字符，并允许使用字符计时器。如果你的应用程序始终读取固定数量的字符，或者连接的设备发送字符流，应使用这种模式。

### 2.3.3 异步输入

上述两种模式都可以以同步和异步模式使用。同步是默认模式，读取语句将阻塞，直到读取完成。在异步模式下，读取语句将立即返回并向调用完成发送信号。该信号可以由信号处理程序接收。

### 2.3.4 等待多源输入

这不是不同的输入概念，但如果你正在处理多个设备，它可能有用。在我的应用程序中，我正在同时处理来自`TCP/IP Socket`的输入和来自另一个进程的串口连接输入。下面的示例将等待两个不同输入源输入。如果一个源可用，它将被处理，然后程序将等待新输入。

描述并不完整，但鼓励你通过这些示例来为你的应用程序推导出最佳解决方案。
不要忘记给串口赋予正确的权限（例如：`chmod a+rw /dev/ttyS1!`）。

## 3.1 规范化输入处理

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <termios.h>
#include <stdio.h>

/* 波特率设置在 <asm/termbits.h> 中，该文件被 <termios.h> 包含 */

#define BAUDRATE 38400

/* 修改此定义以匹配正确的端口 */

#define MODEMDEVICE "/dev/ttyS1"

#define _POSIX_SOURCE 1 /* POSIX 兼容源 */

#define FALSE 0

#define TRUE 1

volatile int STOP=FALSE;

main() {

    int fd,c,res;

    struct termios oldtio,newtio;

    char buf[256];

/*

以读写模式打开调制解调器设备，且不作为控制终端 tty

因为我们不想在 linenoise 发送 CTRL-C 时被杀死。

*/

    fd = open(MODEMDEVICE, O_RDWR | O_NOCTTY);

    if (fd < 0) perror(MODEMDEVICE), exit(-1);

    tcgetattr(fd,&oldtio); /* 保存当前的串口设置 */

    bzero(&newtio, sizeof(newtio)); /* 清空结构体以设置新端口 */

BAUDRATE: 设置波特。你也可以使用 cfsetpeed 和 cfispeed。

CRTSCTS : 输出硬件流控（仅当电缆包含所有必要线路时使用。参见 Serial-HOWTO 第 7 节）

CS8 : 8n（8位数据，无校验，1位停止位）

CLOCAL : 本地连接，无调制解调器控制

CREAD : 启用接收字符
```

```c
/*

newtio.c_cflag = BAUDRATE | CRTSCTS | CS8 | CLOCAL | CREAD;

*/

/*

IGNPAR : 忽略带有校验错误的字节

ICRNL : 将 CR 映射为 NL（否则另一台计算机上的 CR 输入将不会终止输入）

否则将设备设置为原始模式（无其他输入处理）

*/

newtio.c_iflag = IGNPAR | IANL;

/*

原始输出。

*/

newtio.c_oflag = 0;

/*

ICANON : 启用规范化输入

禁用所有回显功能，并且向调用进程发送信号

*/

newtio.c_iflag = ICANON;

/*

初始化所有控制字符

默认值可以在 /usr/include/termios.h 中找到，并在注释中给出，

但我们这里不需要它们

*/

newtio.c_cc[VINTR] = 0;      /* Ctrl-c */

newtio.c_cc[VQUIT] = 0;      /* Ctrl-\ */

newtio.c_cc[VERASE] = 0;    /* del  */

newtio.c_cc[VKILL] = 0;      /* @    */

newtio.c_cc[VEOF] = 4;       /* Ctrl-d */

newtio.c_cc[TIME] = 0;      /* 字符间计时器未使用 */

newtio.c_cc[VMIN] = 1;      /* 阻塞读取直到 1 个字符到达 */

newtio.c_cc[VSTC] = 0;      /* '00' */

newtio.c_cc[START] = 0;   /* Ctrl-q */

newtio.c_cc[VSTOP] = 0;      /* Ctrl-s */

newtio.c_cc[VSUSP] = 0;      /* Ctrl-z */

newtio.c_cc[VEOL] = 0;      /* '\0' */

newtio.c_cc[VPRINT] = 0; /* Ctrl-r */

/*

现在清理调制解调器线路并激活端口设置

*/

tcflush(fd, TCIFUSH);

tcsetattr(fd, TCSANOW,&newtio);

/*

终端设置完成，现在处理输入

在此示例中，在行首输入 'z' 将退出程序。

*/

while (STOP==FALSE) { /* 循环直到满足终止条件 */

/* read 会阻塞程序执行，直到输入行字符，

即使输入了超过 255 个字符。如果字符数少于可用字符数，

后续读取将返回剩余字符。res 将是实际读取的字符数 */

res = read(fd,buf,255);

buf[res]=0; /* 字符串结束，以便我们可以使用 printf */

printf("%s:%d\n", buf, res);

if (buf[0]=='z') STOP=TRUE;

}

/* 恢复旧设置 */

tcsetattr(fd, TCSANOW,&oldtio);
```

## 3.2 非规范化输入处理

非规范化输入模式下，输入不会被组成行，且不会发生输入处理（删除、杀死等）。有两个参数控制这种行为：`c.cc[TIME]`设置字符时间，`c.cc[VMIN]`设置读取前需要接收的最小字符数。

- 如果`MIN > 0`且`TIME = 0`，`read`立即刻满足条件。`TIME`不被使用。
- 如果`MIN = 0`且`TIME > 0`，`TIME`作为超时。如果读取了单个字符，`read`将满足条件。
- 如果`MIN > 0`且`TIME > 0`，`TIME`作为字符间计时器。如果接收到字符或两个字符之间的时间超过`TIME`，`read`将满足条件。每接收到一个字符计时器就会重启，并在接收到第一个字符后激活。
- 如果`MIN = 0`且`TIME = 0`，`read`将立即返回当前可用的字符数。根据上述模式，可以在读取之前通过`fcntl(fd, SETFL)`获取相同的结果。修改`newtio.cc[TIME]`和`newtio.cc[VMIN]`所有模式均有效。

## 程序示例

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <termios.h>
#include <stdio.h>

#define BAUDRATE 38400

#define MODEMDEVICE "/dev/ttyS1"

#define POSIX_SOURCE 1

#define FALSE 0

#define TRUE 1

volatile int STOP=FALSE;

main()

{

    int fd, res;

    struct termios oldtio,newtio;

    char buf[255];

/* 以非阻塞模式打开设备（read 将立即返回） */

    fd = open(MODEMDEVICE, O_RDWR | O_NOCTTY | O_NONBLOCK);
```
