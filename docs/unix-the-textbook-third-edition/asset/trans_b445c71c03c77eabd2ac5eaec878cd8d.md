

```
0x0000000000400951 in get_input (prompt=0x400a76 "Enter a string:
", str=0x0) at bugged.c:30
30         for (*str = getchar(); *str != '\n'; *str = getchar())
(gdb) whatis str
type = char *
(gdb) print s_val
$1 = 0x0
(gdb) print str
$1 = 0x0
(gdb)
```

## 17.7.1.9 修复错误

在发现程序在第 30 行出现故障后，你应该做的第一件事是确定导致故障的语句中涉及的变量。然后你应该显示这些变量的值。

会话立即显示传递给 get_input() 函数的实际参数 s_val 的值为 nil（0）。这导致 get_input() 函数中的形式参数 str 的初始值也为 nil。当我们解引用 str 变量以存储用户输入时，我们尝试访问地址为 0 的内存位置。该位置属于 UNIX 内核空间，用于存储操作系统的常驻部分。因此，进程尝试写入超出其地址空间的、即不属于它的位置。这次尝试是一种明显的违规行为，会导致向正在运行的程序发送 SIGSEGV 信号，从而导致其终止——这是该信号的默认操作。因此，当你从命令行运行程序时，你会看到错误信息 Segmentation Fault。图 17.15 说明了段错误。

要修复程序中的错误，你所需要做的就是将 s_val 指针初始化为已分配给程序的内存空间，静态或动态分配。我们使用一个名为 user_input[SIZE] 的字符数组，并将 s_val 指针设置为指向

![](img/02e070097d401d3bf7de4bf1c470b267_810_0.png)

图 17.15 导致程序失败的内存（段）访问违规。

数组的第一个字节。修订后的 main() 函数如下所示，其中包括其编译和正确执行。代码中的更改是程序中第 8 行、第 17 行和第 19 行的添加，内容如下。

```
% nl -ba working.c
1   /*
2    * Sample C program bugged with a nasty error
3    */
4
5   #include <stdio.h>
6
7   #define PROMPT "Enter a string: "
8   #define SIZE  255
9
10  void get_input(char *, char *);
11  void null_function1 ();
12  void null_function2 ();
13
14  int main ()
15  {
16      char *s_val, *temp;
17      char user_input[SIZE];
18
19      s_val = user_input; /* Initialize s_val to an array */
20      temp = s_val;
21      null_function1 ();
22      null_function2 ();
23      get_input(PROMPT, temp);
24      (void) printf("You entered: %s\n", s_val);
25      (void) printf("The end of buggy code!\n");
26      return (0);
27  }
28
29  void get_input(char *prompt, char *str)
30  {
31      (void) printf("%s", prompt);
32      for (*str = getchar(); *str != '\n'; *str = 
33          getchar())
34          str++;
35      *str = '\0'; /* string terminator */
36  }
37
38  void null_function1 ()
39  { }
40  void null_function2 ();
```
```
41      { }
42
% cc bugged.c -o working
% working
Enter a string: Hello World!
You entered: Hello World!
The end of buggy code!
%
```

## 17.7.1.10 离开 gdb 并收尾

你可以使用 quit 命令离开 gdb 并返回到你的 shell。

```
(gdb) quit
%
```

一旦你的代码经过调试，你就可以通过从二进制文件中删除由 C 编译器的 -g 选项生成的、供调试和性能分析工具使用信息来减小二进制文件的大小，从而释放一些磁盘空间。你可以通过使用 strip 命令来做到这一点。从文件中剥离的信息包含符号表和重定位、调试和性能分析信息。在以下会话中，我们展示了在执行 strip 命令之前和之后的 working 文件的长列表。请注意，文件大小已从 8318 字节减少到 5552 字节，节省了约 33% 的磁盘空间。或者，你也可以使用各种选项重新编译源代码以生成优化的可执行文件。

```
% ls -l working
-rw-r--r--x 1 sarwar faculty 8318 Nov 10 08:25 working
% strip working
% ls -l working
-rw-r--r--x 1 sarwar faculty 5552 Nov 10 08:27 working
%
```

在下面的章节练习中，你将大量使用 gdb 来了解其各种功能。

### EXERCISE 17.22

浏览本节讨论的所有 gdb 命令，以欣赏 gdb 的工作原理。如果本节中使用的某些命令在你的系统上不起作用，请使用 help 命令列出 gdb 命令，并使用你所使用的 gdb 版本中可用的命令。

## 17.7.2 运行时间性能

程序或任何 shell 命令的运行时间性能可以使用 time 命令进行测量和显示。该命令报告三个时间：实际时间、系统时间和用户时间，格式为小时:分钟:秒。实际时间是所花费的实际时间

