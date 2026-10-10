
`0x000011a9 <+0>`: push  ebp

`0x000011aa <+1>`: mov   ebp,esp

`0x000011ac <+3>`: push  ebx

`0x000011ad <+4>`: sub   esp,0194

最后一个被调用的函数在返回到调用程序之前，会通过增加 ESP 到 EBP 来清理栈，这实际上是作为语句的一部分清空了栈。然后，保存的 EIP 会从栈中弹出，作为返回过程的一部分。这被称为函数尾部分（epilogue）。如果一切顺利，EIP 仍然持有下一个要获取的指令，程序将继续执行函数调用之后的语句。

在汇编代码中，尾部分看起来如下：

```
0x000011f3 <+74>: leave
0x000011f4 <+75>: ret
```

在寻找缓冲区溢出时，你会不断看到这些短小的汇编代码。

### 缓冲区溢出

现在你已经掌握了基础知识，我们可以进入正题了。正如第 2 章所述，缓冲区被用于在内存中存储数据。我们主要关注持有字符串的缓冲区。缓冲区本身没有限制机制来阻止你添加比预期多的数据。事实上，如果你作为一个程序员时得于大意，你可以迅速地扩大分配的空间。例如，以下代码在内存中声明了一个长度为 10 字节的字符串：

`char str1[10];`

如果执行以下操作会发生什么？

`strncpy(str1, "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA");`

让我们来发现一下：

```c
//overflow.c
#include <string.h>
int main(){
    char str1[10];
    //声明一个 10 字节的字符串
    //接下来，将 35 字节的"A"拷贝到 str1
    strncpy(str1, "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA");
    return 0;
}
```

现在我们需要编译并执行这个 32 位程序。
由于我们位于 64 位的 Kali Linux 上，首先需要安装 `gcc-multilib` 来交叉编译 32 位二进制文件：

```
$ sudo apt update && sudo apt install gcc-multilib
```

安装 `gcc-multilib` 后，下一步是使用 `-m32` 和 `-fno-stack-protector` 编译我们的程序，以禁用栈金丝虫保护：

```
$ gcc -m32 -fno-stack-protector -o overflow overflow.c
$ ./overflow
zsh: segmentation fault    ./overflow
```

> 注意：在 Linux 风格操作系统中，值得注意的是提示符的约定，这有助于你区分用户 shell 和根 shell。通常，根级 shell 的提示符中包含 `#` 号，而用户 shell 的提示符中通常包含 `$` 号。这是一个视觉提示，显示你何时已成功提升了权限，但你仍然希望使用 `whoami` 或 `id` 等命令来验证这一点。

为什么你得到了段错误（segmentation fault）？让我们通过启动 gdb（GNU 调试器）来看看：

```
$ gdb -q overflow
Reading symbols from overflow...
(No debugging symbols found in overflow)
(gdb) r
Starting program: /home/kali/GHHv6/ch10/overflow
Program received signal SIGSEGV, Segmentation fault.
0x41414141 in ??
(gdb) info reg eip
ip            0x41414141      0x41414141
(gdb) quit debugging session is active.
Inferior 1 [process 7790] will be killed.
Quit anyway? (y or n)
```

如你所见，当你在 gdb 中运行程序时，它在尝试执行 `0x41414141` 处的指令时崩溃，而该地址恰好是 AAAA 的十六进制表示（A 在十六进制中是 `0x41`）。接下来，你可以检查 EIP 是否被 A 损坏了。确实，EIP 充满了 A，程序注定会崩溃。记住，当函数（在此例中为 `main`）尝试返回时，保存的 EIP 值会从栈中弹出并执行。因为地址 `0x41414141` 超出了你的进程段，所以你得到了段错误。

注意：地址空间布局随机化（ASLR）通过随机化程序内存中不同部分的位置工作，包括可执行基础、栈、堆和库，使得攻击者难以可靠地跳转到特定的内存地址。要禁用 ASLR，请在命令行运行：`echo 0 | sudo tee /proc/kernel/randomize_va_space`

现在，让我们来看看 `meet.c`。

# 实验 10-1：溢出 meet.c

你在第 2 章中接触到了 `meet.c` 程序。它看起来如下：

```c
//meet.c
#include <stdio.h>
#include <string.h>
void greeting(char *temp1,char *temp2) {
    char name[400];    //用于存储名字的字符串变量
    strcpy(name, temp2); //将函数参数拷贝到 name
    printf("Hello %s\n", temp1, name); //打印问候语
}
int main(int argc, char *argv[]) {
    greeting(argv[1], argv[2]); //调用函数，传递标题和名字
    printf("Bye %s\n", argv[1], argv[2]); //说再见
    return 0; //退出程序
}
```

我们将使用 Python 来溢出 `meet.c` 中的 400 字节缓冲区。Python 是一种解释型语言，这意味着你不需要预编译它，这使得在命令行中使用它非常方便。目前，你只需要理解一个 Python 命令：

`python -c 'print("A"*600)'`

该命令将简单地向标准输出（stdout）打印 600 个 A——试一下！

**注意**：命令中使用了反引号（`` ` ``）。

让我们编译并执行 `meet.c`：

```
$ gcc -m32 -fno-stack-protector -o overflow overflow.c
$ ./overflow
```

```
(gdb) d 1
(gdb) run Mr `python -c 'print("A*405")'`
Starting program: /home/kali/GHv6/ch10/meet Mr `python -c 'print("A*405")'`
Hello Mr
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
Program received SIGSEGV, Segmentation fault.
main(argc=0, argv=0x) at meet.c:11
11    printf("%s %s\n", argv[1], argv[2]); // say "bye"
(gdb) info regb eip
ebp        0xffffff0041        0xffffff0041
eip        0x56555621e<main+47>
(gdb) run `python -c 'print("A*408")'`
Program received SIGSEGV, Segmentation fault.
0x565556202 in main(argc=<error reading variable: Cannot access memory at address>
0x41414149, at meet.c:10
```
