
```c
#include <stdio.h>

#include <stdlib.h>

#include <unistd.h>

#include <ntpvm.h>

#define MAX_LINE_SIZE 100

static char *typename[] = {"Start Task", "Data", "Broadcast", "Done",

  "Terminate", "Barrier"};

int main(void) {

	char buf[MAX_PACK_SIZE + MAX_LINE_SIZE];

	int bytesread;

	taskpacket_t pack;

	int wsize;

	wsize = sizeof(taskpacket_t);

	printf(stderr, "***** Waiting for first packet\n");

	for(;; ) {

  bytesread = read(STDIN_FILENO, &pack, wsize);

  if (bytesread == 0) {

    fprintf(stderr, "End-of-file received\n");

    break;

  }

  if (bytesread == wsize) {

    fprintf(stderr, "Error reading packet header\n");

    return 1;

  }

  if (pack.type < 0) || (pack.type >= NUMTYPES) {

    fprintf(stderr, "Got invalid packet\n");

    return 1;

  }

  printf("Received packet header of type %d, %s\n", typename[pack.type]);

  printf("compid = %d, taskid = %d, length = %d\n", pack.compid, pack.taskid, pack.length);

  fflush(stdout);

  if (pack.length > MAX_PACK_SIZE) {

    fprintf(stderr, "Task data is too long\n");

    return 1;

  }

  if (read(STDIN_FILENO, buf, pack.length) != pack.length) {

    fprintf(stderr, "Error reading packet data\n");

    return 1;

  }

  write(STDOUT_FILENO, buf, pack.length);

  fprintf(stderr, "***** Waiting for next packet\n");

  }

  return 0;

}
```

### 示例 17.6

以下命令提示包的字段。然后它将包以 ASCII 格式回显到标准输入。

- `a2ts | ts2a`

示例 17.6 中的 `a2ts` 程序交互式地提示包信息并将信息作为二进制包写入其标准输出。`a2ts` 的输出通过管道传递给 `ts2a` 的输入。`ts2a` 程序从标准输入读取二进制包并以 ASCII 格式输出到其标准输出。输入到 `a2ts` 的内容将与 `ts2a` 的输出交织，但这不应该产生问题，因为在 `a2ts` 接收到整个包之前，`ts2a` 不产生任何输出。

### 示例 17.7

以下命令显示了测试分发器（dispatcher）的一种可能方法。目前，使用示例 17.4 中的 `testpacket` 程序代替分发器。

```
a2ts | dispatcher | ts2a
```

示例 17.7 将 `a2ts` 的标准输出重定向到分发器的标准输入，并将分发器的标准输出交给 `ts2a`。示例 17.7 的命令行允许用户输入 ASCII 数据并将任务包显示为 ASCII。遗憾的是，实际测试会从不同来源产生大量数据，难以区分来自不同程序的信息。使用 `a2ts` 的输入和 `ts2a` 的输出将与发送到标准错误的错误信息混合在一起。接下来的两个节提出了处理此问题的两种方法。

## 17.4. 多窗口测试

在测试分发器时，提高 `a2ts` 和 `ts2a` 可用性的第一个策略是使用独立的窗口，如图 17.6 所示。运行在分发窗口中的分发器将其标准输入重定向到命名管道 `inpipe`，其标准输出仍然出现在命名管道 `outpipe` 中。分发器标准错误的输出仍然出现在分发窗口中。`a2ts` 程序从输入窗口的标准输入读取并写入其标准输出，该标准输出被重定向到命名管道 `inpipe`。在此窗口中以 ASCII 格式输入数据包。`ts2a` 将其标准输入重定向到命名管道 `outpipe`。随着分发器的运行，`ts2a` 在输出窗口中显示分发器的输出。

图 17.6 显示了三个窗口的设置。确保三个窗口使用相同的工作目录。运行分发器的步骤如下：

> 图 17.6. 使用三个窗口调试 NTPVM 分发器。

```
$ a2ts > inpipe
```
输入窗口

```
$ mkfifo outpipe
$ mkfifo inpipe
$ dispatcher < inpipe > outpipe
```
分发窗口

```
$ ts2a < outpipe
```
输出窗口

管道

- 1. 在分发窗口中执行以下命令创建两个命名管道。

```bash
mkfifo outpipe
mkfifo inpipe
```

- 2. 在分发窗口中执行以下命令启动分发器。

```bash
dispatcher < inpipe > outpipe
```
此窗口仅显示分发器发送到标准错误的消息，因为标准输入和标准输出都已重定向。

- 3. 在输出窗口中，执行以下命令。

```bash
ts2a < outpipe
```
此窗口显示来自分发器标准输出的数据包。

- 4. 在输入窗口中执行以下命令。

```bash
a2ts > inpipe
```

此窗口显示用户输入数据包的提示符。`a2ts` 程序将输入的信息从 ASCII 转换为数据包格式，并写入分发器的标准输入。

图 17.7 显示了调试的窗口布局。如果你没有支持多窗口的工作站，请尝试说服你的系统管理员安装如 `screen` 的程序，它支持在 ASCII 终端上使用多个屏幕。

## 图 17.7. 调试分发器的逻辑过程布局。

![](img/74e4d4cf6f07ca029fcde95b6b423fe7_697_0.png)

## 17.4.2 远程日志测试

测试分发器的第二种策略使用了第 10.3.4 节和附录 D 中讨论的远程日志设施。用程序 17.4 中的 `ts2log` 程序替换 `ts2a` 程序。`ts2log` 程序使用了附录 B 中描述的重启库中的 `r_readblock` 函数。

## 示例 17.8

以下命令显示了如何使用远程日志测试分发器。

```bash
a2ts | dispatcher | ts2log
```

分发器也应该记录事件。它可以将数据包发送到标准输出，让 `ts2log` 程序通过重定向接收它们。或者，分发器也可以直接记录它们。

## 示例 17.4 ts2log.c

一个使用远程日志工具记录数据包的程序。省略了一些错误检查。

```c
#include <stdio.h>

#include <stdlib.h>

#include <unistd.h>

#include "ntpvm.h"

#include "restart.h"

#include "logging.h"

#define MAX_LINE_SIZE 100

static char typename[] = {"Start", "Data", "Broadcast", "Done",

"Terminate", "Barrier"};

int main(void) {

    char buf[MAX_PACK_SIZE + MAX_LINE_SIZE];

    int bytesread;

    LFILE *lf;

    taskpacket_t *pack;

    int wsize;

    wsize = sizeof(taskpacket_t);

    lf = lopen(NULL,0);

    if (lf == NULL)

        fprintf(stderr, "Failed to open remote logger.\n");

    for(; ; ; ) {

        bytesread = readblock(STDIN_FILENO, &pack, wsize);

        if (bytesread == 0) {

            lprintf(lf, "End-of-file received\n");

            break;

        }

        if (bytesread != wsize) {

            lprintf(lf, "Error reading packet\n");

            continue; // 根据OCR上下文进行逻辑修正

        }

        if (pack->type < 0 || pack->type >= NUMTYPES) {

            fprintf(stderr, "Got invalid packet\n");

            return 1;

        }

        lprintf(lf, "Received packet of type %s\n compid = %d\n taskid = %d\n length = %d\n",

            typename[pack->type], pack->compid, pack->taskid, pack->length);

        if (pack->length > MAX_PACK_SIZE) {

            lprintf(lf, "Task data is too long\n");

            return 1;

        }

        if (readblock(STDIN_FILENO, buf, pack->length) != pack->length) {

            lprintf(lf, "Error reading data\n");

            return 1;

        }

        lprintf(lf, buf);

    }

    return 0;

}
```
