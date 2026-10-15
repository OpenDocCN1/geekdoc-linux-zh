
Unix 系统上 C 语言编程的首选调试器是 `gdb`。它提供了一个强大的命令行界面，允许你在运行程序的同时保持完全控制权。例如，你可以在程序执行过程中设置断点，并在任何位置监控内存或寄存器的内容。因如此，像 `gdb` 这样的调试器对程序员和黑客来说都是无价之。对于那些在 Linux 上寻找更具图形化调试体验的用户，可以使用 `ddd` 和 `edb` 等替代方案或扩展。

### gdb 基础

`gdb` 中常用的命令列在表 2-6 中并进行了描述。

## 实验 2-9：调试

为了调试我们的示例程序，首先在你的 Kali 实例中安装 `gdb`：

```bash
(kali@kali) - [~/GHHv6/ch02]
$ sudo apt-get update
Get:1 http://kali.download/kali kali-rolling InRelease [30.5 kb]
...truncated for brevity...
```

```bash
Reading package lists... Do
(kali@kali)-[~/GHHv6/ch02]
$ sudo apt install gdb
Reading package lists... Do
...truncated for brevity...
Do you want to continue? [Y/n] libc6
Get:1 http://kali.download/kali kali-rolling/main amd64 libc6-i386 amd64
2.31-9 [2,819 kb]
...truncated for brevity...
```

现在，我们执行以下命令。第一条命令将带有调试符号和其他有用选项重新编译我们的 `meet` 程序（请参考表 2-3）。

```bash
(kali|kali) - ~[/GHHv6/ch02]
$ gcc -g -mpreferred-stack-boundary=4 -fno-stack-protector -o meet.c
(kali|kali) - ~[/GHHv6/ch02]

$ gdb meet
Reading symbols from meet...
```

```bash
(gdb) run 1337 Haxor
Starting program: /home/kali/GHHv6/ch02/meet 1337 Haxor
Hello 1337 Haxor
Bye 1337 Haxor
(Inferior 1 (process 17417) exited normally)
(gdb) b main
Breakpoint 1 at 0x5555555555ab: file meet.c, line 10.
(gdb) run 1337 Haxor
Starting program: /home/kali/GHHv6/ch02/meet 1337 Haxor
```

```bash
Breakpoint 1, main (argc=3, argv=0x7fffffe4888) at meet.c:10
10     greeting(argv[1], argv[2]); // call function, pass title & name
(gdb) n
Hello 1337 Haxor
11     printf("Bye %s %s\n", argv[1], argv[2]); // say "bye"
(gdb) n
Bye 1337 Haxor
12     }
(gdb) p argv[1]
$1 = 0x7fffffe719 "1337"
(gdb) p argv[2]
$2 = 0x7fffffe71c "Haxor"
(gdb) p argc
```

| Num | Type | Disp | Enb | Address | What |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | breakpoint | keep | y | 0x0000555555555ab | in main at meet.c:10 |
| | | | | | breakpoint already hit 1 time |

```bash
(gdb) info reg
rax 0
rbx 0
rcx 0
rdx 0
rsi 0x55555555592a 938249922526
...truncated for brevity...
(gdb) quit
A debugging session is active.

Do you still want to close the debugger?(y)
```

## 实验 2-10：使用 gdb 进行反汇编

要使用 `gdb` 进行反汇编，你需要以下命令：

```bash

set disassembly-flavor <int>

disassemble <function>

```

第一条命令在 Intel (NASM) 和 AT&T 格式之间切换。`gdb` 默认使用 AT&T 格式。第二条命令反汇编指定的函数（例如，要用两种格式反汇编 `greeting`，请输入）：

```bash

(kali) - [~/GHHv6/ch02]

$ gdb meet

Reading symbols from meet...

(gdb) disassemble greeting

dump of assembler code for function greeting:

0x000000000000145 <+0>:    push   rbp

0x000000000000146 <+1>:    mov    rsp,rbp

0x000000000000149 <+4>:    sub    $xa0,rsp

0x000000000000150 <+11>:   mov    rdi,-0x18(%rbp)

0x000000000000157 <+18>:   mov    rsi,-0xa0(%rbp)

0x00000000000015e <+25>:   mov    -0xa0(%rbp),rdx

0x000000000000165 <+32>:   lea    -0x19(%rbp),rax

0x00000000000016c <+39>:   mov    rdi,rsi

0x00000000000016f <+42>:   mov    rax,rdi

0x000000000000172 <+45>:   call   0x1030 <strcpy@plt>

0x000000000000177 <+50>:   lea    -0x19(%rbp),rdx

0x00000000000017e <+57>:   mov    -0x18(%rbp),rax

0x000000000000185 <+64>:   mov    rax,rsi

0x000000000000188 <+67>:   lea    0xe75(%rip),rdi

0x000000000000118f <+74>:   mov    $0x0,$esp

0x0000000000001194 <+79>:   call   0x1040 <printf@plt>

0x000000000000119a <+85>:   nop

0x000000000000119b <+86>:   ret

End of assembler dump.

(gdb) set disassembly-flavor intel

(gdb) disassemble greeting

dump of assembler code for function greeting:

0x0000000000001145 <+0>:    push   rbp

0x0000000000001146 <+1>:    mov    rsp,rbp

0x0000000000001149 <+4>:    sub    rsp,0xa0

0x0000000000001150 <+11>:   mov    rdi,-0x18(%rbp)

0x0000000000001157 <+18>:   mov    rsi,-0xa0(%rbp)

0x000000000000115e <+25>:   mov    -0xa0(%rbp),rdx

0x0000000000001165 <+32>:   lea    -0x19(%rbp),rax

0x000000000000116c <+39>:   mov    rdi,rsi

0x000000000000116f <+42>:   mov    rax,rdi

0x0000000000001172 <+45>:   call   0x1030 <strcpy@plt>

0x0000000000001177 <+50>:   lea    -0x19(%rbp),rdx

0x000000000000117e <+57>:   mov    -0x18(%rbp),rax
```
