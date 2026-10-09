
```c
    /* 读取文件内容。 */

    fd = open(filename, O_RDONLY);

    length = read(fd, arg_list, sizeof(arg_list));

    close(fd);

    /* read 不会对缓冲区进行 NUL 终止处理，因此在这里处理。 */

    arg_list[length] = '\0';

    /* 遍历参数。参数由 NUL 分隔。 */

    next_arg = arg_list;

    while (next_arg < arg_list + length) {

        /* 打印参数。每个参数都以 NUL 终止，因此将其
        视为普通字符串处理。 */

        printf("%s\n", next_arg);

        /* 移动到下一个参数。由于每个参数都
        以 NUL 终止，strlen 统计的是下一个参数的长度，
        而不是整个参数列表。 */

        next_arg += strlen(next_arg) + 1;

    }

}

int main(int argc, char *argv[]) {

    pid_t pid = (pid_t) atoi(argv[1]);

    print_process_arg_list(pid);

    return 0;

}
```

例如，假设进程 `372` 是系统日志守护进程 `syslogd`。

```bash
% ps 372
PID TTY      STAT TIME COMMAND
372 7       S 0:00 syslogd -m 0

./print-arg-list 372
```

```
syslogd
-m
0
```

在这种情况下，`syslogd` 被调用时带有参数 `-m`。

### 7.2.3 进程环境

`environ` 变量包含了进程的环境（参见第 2.1.6 节，“环境”）。与 `cmd` 类似，各个环境变量之间由 `NUL` 分隔。每个元素的格式与 `environ` 变量使用的格式相同，即 `VARIABLE=value`。

列表 7.4 展示了第 2.1.6 节列表 2.3 中程序的通用版本。该版本在命令行上接受一个进程 ID，并通过读取 `/proc` 来打印该进程的环境。

列表 7.4 (`print-environment.c`) 显示进程的环境

```c
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

/* 打印 PID 指定进程的环境，每个环境变量独占一行。 */

void process_environment (pid_t pid)

{

    int fd;

    char filename[24];

    char environment[8192];

    size_t length;

    char* next_var;

    /* 生成进程的环境文件名。 */

    snprintf(filename, sizeof(filename), "/proc/%d/environ", (int) pid);

    /* 读取文件内容。 */

    fd = open(filename, O_RDONLY);

    length = read(fd, environment, sizeof(environment));

    close(fd);

    /* read 不会对缓冲区进行 NUL 终止处理，因此在这里处理。 */

    environment[length] = '\0';

    /* 遍历变量。变量由 NUL 分隔。 */

    next_var = environment;

    while (next_var < environment + length) {

        /* 打印变量。每个变量都以 NUL 终止，因此只需
           视为普通字符串处理。 */

        printf("%s\n", next_var);

        /* 移动到下一个变量。由于下一个变量以
           NUL 终止，strlen 统计的是下一个参数的长度， */

        next_var += strlen(next_var) + 1;

    }

}
```

### 7.2.4 进程执行文件

`exe` 项指向可执行文件。在第 2.1.1 节中，我们解释过 `exe` 项是指向程序的符号链接。但注意，通过检查 `/proc/self/exe`，你可以找到调用进程的路径。这是确定可执行文件位置的一种有用技术。

列表 7.5 (`get-executable-path.c`) 获取可执行文件的路径

```c
#include <limits.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>

/* 查找可执行文件的路径。 */

void get_executable_path(char* buffer) {

    int fd;

    fd = open("/proc/self/exe", O_RDONLY);

    size_t length = read(fd, buffer, sizeof(buffer) - 1);

    close(fd);

    buffer[length] = '\0';

}

int main() {

    char path[PATH_MAX];

    get_executable_path(path);

    // ... (代码其余部分)

}
```

### 7.2.5 文件描述符

`fd` 子目录包含已打开的文件描述符项。回想我们在第 2.1.4 节“标准 I/O”中提到，文件描述符 `0`、`1` 和 `2` 分别初始化为标准输入、输出和错误。因此，通过向 `/proc/[pid]/fd/1` 写入，你可以向第一个窗口连接到 `stdout` 的设备（在本例中为终端）写入内容。在第二个窗口中，尝试向该文件写入消息：

```bash
% echo 'Hello, world.' >> /proc/1261/fd/1
```

文本出现在第一个窗口。标准输入、输出和错误的文件描述符也出现在 `fd` 子目录中。列表 7.6 显示了一个程序，它只是打开命令行指定的文件描述符，然后无限循环。

列表 7.6 (`open-and-spin.c`) 打开文件读取

```c
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main (int argc, char* argv[]) {

    if (argc < 2) {

        fprintf(stderr, "Usage: %s <filename>\n", argv[0]);

        return 1;

    }

    const char* filename = argv[1];

    int fd = open(filename, O_RDONLY);

    printf("in process %d, file descriptor %d is open to %s\n",

           (int) getpid(), (int) fd, filename);

    while (1) {

        // loop forever

    }

    return 0;

}
```

```
lrwx------      1 samuel samuel    64 Jan 30 01:30 1 -> /dev/pts/2
lrwx------      1 samuel samuel    64 Jan 30 01:30 2 -> /dev/pts/2
lr-x------      1 samuel samuel    64 Jan 30 01:30 3 -> /etc/fstab
```

注意文件描述符 `3` 的项，它链接到在该描述符上打开的 `/etc/fstab` 文件。

文件描述符也可以在套接字或管道上打开（更多信息请参见第 5 章）。在这种情况下，对应文件描述符的符号链接目标将显示“socket”（套接字）或“pipe”（管道），而不是指向普通文件或设备。

## 7.2.6 进程内存统计

`statm` 项包含一个七个数字的列表，用空格分隔。每个数字都代表进程在特定类别中使用的内存页计数。这些类别按照数字出现的顺序列如下：

- 进程总大小
- 驻留在物理内存中的进程大小
- 与其它进程共享的内存——即同时被此进程和至少另一个进程映射的内存（例如共享库或未触碰的写页）
- 进程大小——即已加载的可执行代码大小
- 映射到此进程的共享库大小
- 此进程用于堆栈的内存
- 脏页数量——即被程序修改过的内存页

### 7.2.7 进程统计

`status` 项包含了关于进程的各种信息，采用了便于人类理解的格式。这些信息包括进程 ID (`PID`) 和父进程 ID (`PPID`)、真实和有效用户 ID 及组 ID、内存使用情况以及指定哪些信号被捕获、忽略和阻塞的位掩码。

## 7.3 硬件信息

`/proc` 文件系统中的其他几个项提供了对系统硬件信息的访问。虽然这些项通常对系统配置员和管理员感兴趣，但这些信息有时对应用程序开发人员也有帮助。我们在这里介绍一些更有实用的项。

### 7.3.1 CPU 信息

如前所示，`/proc/cpuinfo` 包含了关于运行 GNU/Linux 系统的 CPU 或 CPU 的信息。`Processor` 字段列出了处理器编号；对于单处理器系统，该值为 0。`Vendor`、`CPU Family`、`Model` 和 `Stepping` 字段允许你确定 CPU 的确切型号和修订。更有用的是 `Flags` 字段显示设置了哪些 CPU 标志，这指示了 CPU 可用的特性。例如，“mmx”表示扩展 MMX 指令可用。

来自 `/proc/cpuinfo` 的大部分信息源自 `cpuid` x86 汇编指令。该指令是程序获取 CPU 信息的底层机制。要更深入地理解 `/proc/cpuinfo` 的输出，请参阅英特尔《IA-32 架构软件开发手册第 2 卷：指令集参考》中 `cp` 指令的文档。该手册可以通过 `http://developer.intel.com/design` 获取。

最后一个元素 `bogsip` 是一个 Linux 特有的值。它是对处理器在紧凑循环中速度的测量，因此不是整体处理器速度的良好指标。

### 7.3.2 设备信息

`/proc/devices` 文件列出了系统可用的字符设备和块设备的设备号。关于设备类型和设备号的信息，请参见第 6 章“设备”。

### 7.3.3 PCI 总线信息

`/proc/pci` 文件列出了连接到 PCI 总线或总线的设备摘要。这些是真实的 PCI 扩展卡，也可能包括系统主板上的设备以及 AGP 卡。列表包含了设备类型；设备 ID 和厂商 ID；设备名称（如果可用）；设备提供的特性信息；以及设备使用的 PCI 资源信息。

### 7.3.4 串口端口信息

`/proc/tty/driver/serial` 文件列出了串口端口的配置信息和统计数据。串口端口从 0 开始编号。可以使用 `setserial` 命令获取并修改串口端口的配置信息。然而 `/proc/tty/driver/serial` 显示了关于每个串口端口中断数的额外统计。

3. 参阅《IA-32 英特尔架构软件开发手册》获取 MMX 指令的文档，并参考本书第 9 章“内联汇编代码”获取如何在 GNU/Linux 程序中使用这些及其他汇编指令的信息。
4. 注意，在 DOS 和 Windows 下，串口端口从 1 开始编号，因此 `COM1` 在 Linux 下对应串口端口号 0。

例如，来自 `/proc/tty/driver/serial` 的行：
（此处省略了重复的示例内容）

## 7.5.2 驱动器与分区

`/proc` 文件系统包含了连接到 IDE 控制器和 SCSI 控制器的设备信息（如果系统包含这些设备）。

在典型系统中，`/proc/ide` 子目录可能包含 `ide0` 和 `ide1` 两个子目录之一，分别对应主、从 IDE 控制器。这些目录包含对应于连接到控制器上的物理设备的进一步子目录。如果 Linux 未识别到任何连接的设备，则控制器或设备目录可能不存在。四个可能的 IDE 设备的完整路径列在表 7.1 所示。

| 控制器 | 设备 | 子目录 |
| --- | --- | --- |
| 主 (Primary) | 主 (Master) | `/proc/ide/ide0/hda/` |
| 主 (Primary) | 从 (Slave) | `/proc/ide/ide0/hdb/` |
| 从 (Secondary) | 主 (Master) | `/proc/ide/ide1/hdc/` |
| 从 (Secondary) | 从 (Slave) | `/proc/ide/ide1/hdd/` |

关于 IDE 设备名称的更多信息，请参见第 6.4 节，“硬件设备”。每个 IDE 设备目录包含多个条目，提供对设备标识和配置信息的访问。这里列出了一些最有用的条目：

- `model` 包含设备的型号标识字符串。
- `media` 包含设备的介质类型。可能值为 `disk`、`cdrom`、`tape`、`floppy` 和 `UNKNOWN`。
- `capacity` 设备的容量，以 512 字节块为单位。注意，对于 CD-ROM 设备，该值将为 $2^{-1}$，而不是驱动器磁盘的容量。注意 `capacity` 中的值代表整个物理磁盘的容量；磁盘分区内文件系统的容量会更小。

例如，这些命令显示了如何确定从 IDE 控制器主设备的介质类型和设备标识。在这种情况下，结果是一个 Toshiba CD-ROM 光驱。

```bash
% cat /proc/ide/ide1/hdc/media
cdrom

% cat /proc/ide/ide1/hdc/model
TOSHIBA CD-ROM QM-6702B
```

5. 如果配置适当，Linux 内核可以支持额外的 IDE 设备控制器。这些控制器从 `ide2` 开始按顺序编号。

## 7.5 驱动器、挂载与文件系统

如果系统中存在 SCSI 设备，`/proc/scsi/scsi` 包含了它们标识值的摘要。例如，内容可能如下所示：

```bash
% cat /proc/scsi/scsi
Attached devices:

Host: scsi Channel: 00 ID: 00 Lun: 00
Vendor: QUANTUM Model: ATLAS_V_9_WLS Rev: 0230
Type: Direct-Access ANSI: SCSI revision: 03

Host: scsi Channel: 00 ID: 04 Lun: 00
Vendor: QUANTUM Model: QM3910TD-SW Rev: N491
Type: Direct-Access ANSI SCSI revision: 02
```

这台计算机包含一个单通道 SCSI 控制器（指定为 `"scsi0"`），连接了两个 Quantum 驱动器，SCSI 设备 ID 分别为 `0` 和 `4`。

`/proc/partitions` 项显示了已识别磁盘设备的分区。对于每个分区，输出包含了主设备号和次设备号、1024 块的数量以及对应于分区的设备名。

`/proc/sys/dev/cdrom/info` 条目显示了关于 CD-ROM 驱动器能力的杂项信息。这些字段是自明的：

```bash
% cat /proc/sys/dev/cdrom/info
CD-ROM information, id: cdrom.c 2.56 1999/09/09

drive name: hdc
drive speed: 48
drive # of slots: 0
Can close tray: 1
Can open tray: 1
Can lock tray: 1
Can change speed: 1
Can select disk: 0
Can read multisession: 1
Can read MCN: 1
Reports media changed: 1
Can play audio: 1
```
