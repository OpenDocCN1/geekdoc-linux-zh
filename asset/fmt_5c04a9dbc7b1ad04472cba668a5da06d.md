
```
% cat sample.c
...
    if (fd == -1) {
        printf("File open failed.");
        exit(0);
        /*NOTREACHED*/
    }
...
%
```

`lint`命令可以使用几个命令行选项运行。例如，`-c`选项检查可疑有效性的类型转换。因此，`lint`对以下代码中的`s = (int *) i;`语句报告警告：

```
$ cat test.c
int main()
{
    char *s;
    int i=100;
    s = (int *) i;
    return(0);
}
% lint test.c
test.c:
test.c(6): warning: illegal pointer combination, op = [124]
test.c(6): warning: s set but not used in function main [191]
lint: cannot find llib-lc.ln
Lint pass2:
$ lint -c test.c
(8) warning: illegal combination of pointer and integer, op CAST
(9) warning: assignment type mismatch: pointer to char "=" pointer to int
$
```

我们强烈建议您在编译模块之前创建一个`make`规则来运行`lint`实用程序。以下是示例`make`规则及其执行：

```
% cat makefile
SOURCES = compute.c input.c main.c
LINTFLAGS = -c
...
lint: $(SOURCES)
```

```
lint $(LINTFLAGS) $(SOURCES)
...
% make lint
lint -c compute.c input.c main.c
...
%
```

虽然`lint`检查了大部分可移植性功能，但它不检查几件事。它不检查`printf`调用中的控制字符串是否与相应变量的类型匹配。它也不确保变量在前七个字符后是唯一的。除了这些小例外，`lint`是无故障的，应该定期使用以从生产软件中去除粘性物质。

## 17.6.2 源代码度量

您可以使用UNIX工具`prof`来显示您的代码配置文件，具体来说是使用的函数和每个函数所花费的时间百分比。此信息允许您更密切地关注导致软件瓶颈的那些函数。

有时，您会想知道程序在每个函数上花费的时间。当程序执行时，您可以使用此信息通过优化它们来提高程序某些部分的性能。UNIX有两个主要工具用于分析程序性能：`prof`和`gprof`。两个工具都允许您的程序跟踪每个函数被调用的次数和每个函数花费的时间。`gprof`工具比`prof`提供更多数据，但两者在识别程序的昂贵部分和执行路径方面都很有效。两个工具的使用非常相似，它们生成类似的输出。我们只讨论`prof`，但显示的步骤也适用于`gprof`。

使用`prof`的第一步是使用特定选项编译您的程序，该选项要求编译器在目标模块中插入适当的代码来计数每个函数执行的次数和每个函数花费的时间。为了完全测试您的程序，请使用`cc`编译器命令并使用`-p`选项，如下所示：

```
% cc -p matrix_mult.c -o mm
%
```

在您的程序成功编译后，运行它。执行会在名为`mon.out`的文件中生成运行时数据，格式为`prof`可以读取的格式。然后您使用此文件中的`prof`实用程序来显示程序配置文件。`gprof`工具在PC-BSD和Solaris上都可用。然而，`prof`仅在Solaris上可用。

## 17.7 动态分析工具

程序的动态分析涉及其在运行时的分析。正如我们之前提到的，这个阶段包括软件的调试、跟踪和性能监控，包括针对产品需求的测试。在本节中，我们将讨论两个有用的UNIX工具，用于跟踪程序的执行和调试（`gdb`），以及以实际时间单位（`time`）测量程序的运行时间。

## 17.7.1 源代码调试

软件调试的任务耗时且困难。它包括在代码执行时监控代码的内部工作，检查程序变量的值和函数返回的值，以及使用特定输入参数执行函数。正如我们之前所说，许多C程序员倾向于在程序的各个地方使用`printf`调用（C++为`cout`）来定位bug的来源然后去除它。这项技术简单，对于小型程序效果很好。然而，对于大型软件，其中错误可能隐藏在函数调用层次结构的深处，此技术最终会花费大量编辑时间来在源文件中添加和删除`printf`（或`cout`）调用。在这种情况下，更有效的调试方法是使用符号调试器。典型的符号调试器提供了几个设施来观察程序的运行时行为，包括以下内容：

- 运行程序
- 设置断点
- 单步执行
- 列出源代码
- 编辑源代码
- 访问和修改变量
- 跟踪程序执行
- 搜索函数和变量
- 识别程序崩溃时正在做什么

UNIX平台上有几个符号调试器，最常见的是免费的GNU调试器，`gdb`。Solaris和PC-BSD上的默认源代码调试器分别是`adb`和`gdb`。它们提供了类似的设施。`adb`是`mdb`的链接，模块化调试器，允许您检查进程、用户进程核心转储以及实时操作系统和操作系统转储。我们主要描述`gdb`，因为它是大多数UNIX系统上的标准调试器。尽管`gdb`也有几个用于调试C++类的功能，但我们只讨论其用于调试C程序的功能。以下是该实用程序的简要描述。

### 语法

```
gdb [options] [executable-file [core-file or PID]]
```

**目的：**允许对使用C或C++源文件生成的**可执行文件**中的程序进行源级调试和执行；或**核心文件**，由于C/C++程序崩溃而创建；或正在运行的程序的进程ID（**PID**）

### 常用选项/功能：

- **`-c file`** 将文件 `file` 作为核心转储进行检查（即 UNIX 在程序崩溃时创建的文件）
- **`-h`** 列出所有选项及其简要说明
- **`-n`** 不从任何 `.gdbinit` 初始化文件运行命令
- **`-x file`** 从文件 `file` 执行 `gdb` 命令（如果未指定 `file`，则从 `.gdbinit` 初始化文件执行）

启动时，`gdb` 会搜索 `.gdbinit`。搜索顺序为：当前目录 `(.)` 然后是主目录 `(~)`。`-x` 选项允许您使用任何文件作为启动文件。表 17.6 给出了一些常用 `gdb` 命令的简要描述。

### 17.7.1.1 使用 gdb

在用 `gdb`（或其他调试器）调试程序之前，您必须使用 `-g` 编译器选项编译它，以便在可执行文件中包含符号表和重定位、调试和剖析信息。此信息由调试和剖析工具使用。我们使用 `bugged.c` 文件中的程序来展示 `gdb` 的各种功能。该程序提示您输入键盘输入，显示输入并退出。我们使用多个函数来演示 `gdb` 在设置断点和在函数边界显示堆栈跟踪、通过逐条执行程序语句跟踪程序执行、查看变量的类型和值等方面的功能。以下会话显示了程序代码、未使用 `-g` 选项编译它以及其执行情况。

```
% nl -ba bugged.c
     1   /*
     2    * Sample C program bugged with a nasty error
     3    */
     4
     5
     6   #include <stdio.h>
     7
     8   #define PROMPT  "Enter a string: "
     9
    10   void get_input(char *, char *);
    11   void null_function1 ();
    12   void null_function2 ();
    13
    14   int main ()
    15   {
    16       char *s_val, *temp;
    17
    18       temp = s_val;
    19       null_function1 ();
     20        null_function2 ();
     21        get_input (PROMPT, temp);
     22        (void) printf ("You entered: %s\n", s_val);
     23        (void) printf ("The end of buggy code!\n");
     24        return (0);
     25    }
     26
    27    void get_input (char *prompt, char *str)
    28    {
```

## 表 17.6 常用 gdb 命令

| 命令 | 简要说明 |
|---|---|
| break | break `<line_num>` : 在行号 `line_num` 处设置断点 |
|  | break `<function_name>` : 在函数 `function_name` 处设置断点 |
| continue | continue : 在断点后继续执行 |
