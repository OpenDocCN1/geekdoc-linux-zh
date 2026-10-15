
# 706 第三部分：Linux 内存取证

## 库注入

向进程注入 shellcode 对于攻击者在初始利用和限制活动中非常有用。编写功能全的软件需要

编写 shellcode 是很困难的，因为它是位置无关的（即没有硬编码地址），并且无法直接依赖 API 调用。为了弥补这种情况，许多程序员选择将他们的后门实现为共享库，并用 C 语言编写它们。

如上文所述，攻击者有两种方法向远程进程注入库。第一种方法简单，使用原生系统 API 将存储在磁盘上的攻击者共享库加载到另一个进程的地址空间中。然而，这种技术会在内存和磁盘中留下许多痕迹。第二种方法加载仅位于内存中的库，从不写入磁盘。这种方法实现起来更容易，但在内存中留下的痕迹较少，且磁盘上没有产物。

### 从磁盘注入库

Linux 加载器提供了 `dlopen`、`dlclose` 和 `dlsym` 等函数，它们分别相当于 Windows 的 `LoadLibrary`、`FreeLibrary` 和 `GetProcAddress` 函数。这些函数共同允许程序员在运行时加载库、卸载库并查询库中的符号地址。要将存储在磁盘上的共享库注入远程进程，恶意进程所做的大部分就是强制目标进程调用 `dlopen`（`dlopen` 封装的函数），其第一个参数是共享库的路径。

> 注意
> 使用 `_dlopen` 而不是 `dlopen` 是因为 `dlopen` 仅存在于通过与运行时加载器交互的应用程序中。另一方面，`_dlopen` 位于 `libc` 内部，加载所有动态链接应用程序的地址空间。在最近版本的 `libc` 中，`dlopen` 也被弃用并替换为 `_libc_mode`。该进程可用于在所有动态链接应用程序中调用此函数，并被 `injectso64` (https://github.com/ice799/injectso64) 等项目使用。

据我们所知，该技术的第一个公开文档见于《运行时进程注入》(http://phrack.org/issues/59/8.html)。在篇文章中，作者使用了之前描述的 `ptrace` 技术将 shellcode 注入进程并随后执行它。该 shellcode 随后以如下方式加载共享库：

```
1 _start:   jmp string

2 begin:     pop      eax      ; char *file

3             xor      ecx      ; *caller

4             mov      edx      ,01 ; int mode

6

7 mov ebx 0x12345678 ; addr of _dlopen()

8 call ebx ; call _dlopen!

9 add esp, 0x4

10

11 int3 ; ; breakpoint

12

13 string: call begin

14 db "/tmp/ourlibby.so",0x00
```

在第 1 行，shellcode 跳转到第 13 行的 `string` 标签。`call begin` 指令将控制权传回第 3 行。这种反射的效果是将 `/tmp/ourlibby.so`（要加载的库路径）的地址放在栈顶。因此，当第 3 行执行 `pop eax` 时，字符串的地址被复制到 `EAX` 寄存器中，并成为 `_dlopen` 的第一个参数。第 7 行持有一个 `_dlopen` 地址的占位值，该值在运行时会被目标进程内函数的真实地址进行修补。在第 8 行，调用了 `_dlopen`，在第 13 行，它执行并将控制权返回给恶意进程。

### 基于检测的共享库注入

你可以使用多种方法检测基于共享库的注入。由于恶意库是以与合法库相同的方式（即通过 `_dlopen`）加载的，内核会为映射映射的文件填充数据结构。因此，你可以使用 `linux_proc_maps` 插件进行检测。在这种情况下，恶意软件向目标进程注入了一个名为 `/tmp/.ICE-unix` 的库。这个文件名具有误导性，因为大多数 Linux 发行版都有一个由 X Server 创建的 `/tmp/.ICE-unix` 目录：

```bash
$ python vol.py -f sharedlib.lime --profile=LinuxDebian3_x86 linux_proc_maps -p 18550

Volatility Volatility Framework 2.4

Pid Start End Flags Pgoff Major Minor Inode File Path

<snip>

18550 0xb7b2b000 0xb7b2b000 r-x 0x0 8 1 1439419 /tmp/.ICE-unix

18550 0xb7b2b000 0xb7b2b000 rw- 0x0 8 1 1439419 /tmp/.ICE-unix

<snip>
```
