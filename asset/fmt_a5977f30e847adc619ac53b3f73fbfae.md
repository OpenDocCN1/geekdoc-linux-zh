
`syslog` 程序与 `socket` 服务器不同，因为 `syslog` 程序预计仅在 IBM i5/OS 上运行。根据此，所有语句都需要明确代码。还需要获取额外数据，如当前时间和传输控制协议/网际 (`TCP/IP`)。最后，必须打开一个文件来存储传入消息并将选定的消息发送到 `QSYSOPR`。

示例 B-2 所示程序流程：

- 打开存储所有消息的文件。如果文件不存在，则创建它。否则，以追加模式打开文件。这确保不会丢失已记录的消息。
- 打开 `socket` 描述符。
- 将端口 `514` 绑定到新的 `socket` 描述符。这是 Linux 使用的端口。如果连接 Linux，IBM i5/OS 程序也需要更改。
- 创建转换表。所有传入数据均来自 Linux，因此从美国标准代码 (`ASCII`) 转换为扩展二进制编码 (`EBCDIC`)。启动程序主体循环直到停止：
    1. 从 `socket` 接收传入请求。
    2. 将数据转换为 `EBCDIC`。
    3. 移除末尾的换行符。
    4. 获取系统信息并将其添加到消息头部。
    5. 检查此消息是否去 `QSYSOPR`，如果是则发送。
    6. 获取时间戳。
    7. 将消息写入日志文件。
    8. 最后刷新缓冲区。
- 在退出程序前关闭转换表和 `socket` 描述符。

## Linux 与 IBM i5/OS 的集成

要创建 `syslogd` 程序，请按顺序运行以下命令：

1. `CRTCMOD (ITSOLIB/SYSLOGD) SRCSTMF('/ifs/src/syslog.c') SRCTYPE(*SRFS) TGTAID(37)`
2. `CRTPGM (ITSOLIB/SYSLOGD) BNDSRVPGM(QSYS/QICONV)`

这些命令在 `ITSOLIB` 库中创建一个名为 `SYSLOGD` 的程序，并假设源码位于集成文件系统 (`IFS`) 中的 `/ifs/src/syslog.c`。你必须根据环境调整对象名称。

运行程序之前的下一步是创建 `IFS` 目录结构。程序会在文件不存在时创建文件，但无法创建所需的完整目录结构。你可以使用 `QSYSOPR` 上的 `mkdir` 命令创建 `/var/log`。你还需要创建一个用于 `QSYSOPR` 消息的消息文件。在我们部署的程序中，消息文件是 `ITSOLIB/LINUX`，只要程序激活，就可以更改以满足你的需求。这些步骤是：

1. `MKDIR DIR(/var/log)`
2. `CRMSGF (ITSOLIB/LINUX) TEXT(Message file for SYSLOGD)`
3. `ADDMMSG MSGID(LNX0001) MSGF(ITSOLIB/LINUX) MSG('&*1') SECLVL('&2') FMT(*CHAR 80) (*BACK 5)`

创建程序和消息文件后，你可以使用以下命令提交 `syslogd` 程序批运行：

```
SBJOB CMD (ALL SYSLOGD/SYSLOGD)
```

批作业现在运行并监控 `514` 端口的传入消息。所有传入消息都记录到文件 `/var/log/messages`，任何包含 "kernel" 的消息也会发送到 `QSYSOPR` 消息队列。

### 示例 B-2 IBM i/OS 上的 `syslogd` 源代码

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#include <errno.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>

#include <iconv.h>
#include <QHMSNDM.H>

#define SERVER_PORT 514
#define BACK_LOG 20
#define BUFFER_SIZE 512

typedef struct {
 char name[8];
 char ccsid[5];
 char conversion[3];
 char substitute[1];
 char shift[1];
 char input[1];
 char option[1];
 char RESERVED[12];
} fromCode;

typedef struct {
char name[8];
char ccsid[5];
char RESERVED[19];
} Code_t;

FILE * openFile(void);
iconv_t createConversionTable(void);
void getDotted(char *dottedName, long ipAddress);
void logMessage(char *message);

int main(int argc, char *argv[])
{
int rc,
bufferLength,
recordCount = 0;
char buffer[BUFFER_SIZE];
converted[BUFFER_SIZE];
message[BUFFER_SIZE];
*inBuffer,
*convertBuffer,
dotted[15];
*logFile;
time_t currentTime;

/* socket() 变量 */
int descriptor,
addressFamily,
type,
protocol;

/* bind() 变量 */
struct sockaddr_in localAddress;
int addressLength;

/* recvfrom() 变量 */
int flags,
clientLength;
struct sockaddr_in clientAddress;

/* gethostbyaddr() 变量 */
struct hostent *system;

/* iconv() 变量 */
size_t inBufferLength,
convertBufferLength;
iconv_t convertTable;
}
```

```c
/* socket() 变量 */
/* bind() 变量 */
/* recvfrom() 变量 */
/* close() 变量 */

/* 打开文件 */
logFile = openFile();

/* 打开 socket 描述符 */
addressFamily = AF_INET;
type = SOCK_DGRAM;
protocol = IPPROTO_IP;
if ((descriptor = socket(addressFamily, type, protocol)) < 0) {
    printf("Error getting socket descriptor\n");
    printf("errno is %i\n", errno);
    exit(-1);
}

/* 绑定到 socket */
memset(&localAddress, 0x00, sizeof(localAddress));
localAddress.sin_family = AF_INET;
localAddress.sin_port = htons(SERVER_PORT);
localAddress.sin_addr.s_addr = htonl(INADDR_ANY);
addressLength = sizeof(localAddress);
if ((rc = bind(descriptor, (struct sockaddr*)localAddress, addressLength)) < 0) {
    printf("Error binding to the socket\n");
    printf("errno is %i\n", errno);
    close(descriptor);
    exit(-1);
}

/* 仅在 OS/400 服务器上设置转换表 */
convertTable = createConversionTable();
```
