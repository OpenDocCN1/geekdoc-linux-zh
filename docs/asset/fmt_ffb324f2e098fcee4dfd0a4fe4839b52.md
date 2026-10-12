
`0436d93` `warn_slowpath_common+0x70/0x87`

`0417a26` ? `native_apic_write_dummy+0x32/0x3e`

`0436dbc` `warn_slowpath_null+0x12/0x15`

`0417a26` ? `native_apic_write_dummy+0x32/0x3e`

`040fd2c` `intel_init_thermal+0xc3/0x168`

`040e8ce` ? `mce_init+0xa9/0xbd`

`040f600` `mce_feature_init+0x10/0x50`

`040dcc9` `mce_cpu_features+0x1b/0x24`

`0760681` `mcheck_init+0x249/0x28b`

```
```

`<075ea6e>` `identify_cpu+0x37f/0x38e`

`<0990265>` `identify_boot_cpu+0xd/0x23`

`<09903df>` `check_bugs+0xb/0xdc`

`<0478a33` ? `delayacct_init+0x47/0x4c`

`<09898aa>` `start_kernel+0x31c/0x330`

`<0989070>` `i386_start_kernel+0x70/0x77`

```
```

现在我们明白了问题所在，可以再次查看 Fedora 示例并尝试理解问题。我们在未维护的内核中遇到了由 `swapper` 进程引起的崩溃。崩溃报告指向 `native_apic_write_dummy` 函数。这是一个很长的跟踪，包含了很多信息，应该帮助我们解决问题。我们将看到如何使用崩溃报告帮助开发者修复 Bug 并产生更稳定的软件。现在让我们更多关注 crash 和基础命令。

### 所有任务的栈回溯 (Backtrace for all tasks)
默认情况下，`crash` 会显示活动任务的栈回溯。但你可能也想查看所有任务的栈回。在这种情况下，你想运行 `foreach`：

```
foreach bt
```

### 转储系统缓冲区 (Dump system buffer)
此命令按时间顺序转储内核 `log_buf`。`log_buf` 可能包含系统崩溃的有用线索。如果你有硬件问题，它可能并不真正有用，但绝对值得尝试。这里是 `crash` 的几行：

```
error: failed opcode: 0ec

type: mismatch for 800000700020, new: write-combining

ISO 9660 Extensions: Microsoft Level 3

ISO 9660 Extensions : RR191A

SysRq : Trigger a crash
```

```
HARDWARE ERROR

CPU 6: Machine Check Exception             5 Bank 3: b62000700021a

RIP !INACT! 33:<00002aac124>

TSC 3324ieebff9 ADDR 7641b070

这不是软件问题！
```

### 显示进程信息 (Display process information)
此命令显示系统内选定或所有进程的状态。如果没有输入参数，则显示所有进程的数据。`crash` 工具可能会加载指向一个没有导致 panic 的任务，或者可能找不到 panic 任务。如果你正在使用虚拟机（包括 VMware 或 Xen），情况可能会变得更加复杂。

```
STATE: TASK_RUNNING

WARNING: panic task not found
```

## 超级技术内容：C 代码分析
我们现在不仅尝试理解崩溃代码报告，还要弄清楚如何在代码层面解决问题。假设你可能想分析违规函数的 C 代码。不言而喻，你应该拥有 C 源码文件并能够读取它们。

## 源代码
好了，你想检查代码。首先，你必须获取源码文件。你也可以访问 Linux 内核存档并下载与你匹配的内核，尽管某些源码可能与你系统上使用的不同，因为某些厂商会进行自定义更改。一旦你有了源码，就是时候检查它们了。

# 崩溃分析 (crash) 185

## Cscope

你可以使用 `grep` 等标准工具浏览源代码，但这可能非常繁琐。一个用于浏览 C 代码的非常实用的工具叫做 `cscope` (Cscope, n.d.)。该工具从命令行运行，并使用类 vi 界面。默认情况下，它会搜索当前目录下的源文件，但你可以按任何方式进行配置。现在，在包含源文件的目录（默认是 `/usr/src/linux`）中运行 `cscope`：

```
cscope -R
```

Copyright ©Intel Corporation. All rights reserved.

这将递归地搜索所有子目录，索引源代码并显示主界面。它还有其他用途；请尝试 `man` 页面或 `--help`。第一次启动时，`cscope` 将花费一些时间建立索引。在主界面上，你可以搜索所需的符号、全局定义、函数、字符串和其他信息，如图 6.3 所示。

我们将从“查找此 C 符号”开始。使用方向键移动到这一行，输入所需的函数名并按回车。结果将显示出来，如图 6.4 所示。

根据情况，你可能会得到很多结果或一个结果。崩溃报告中可能没有包含该函数的源代码。如果结果太多，你可能想通过“查找调用此函数的函数”选项来搜索调用跟踪中的下一个函数。使用 `Tab` 键在输入区域和输出区域之间跳转。如果你有官方供应商支持，现在是把命令交给他们并让他们来主导的好时机。

如果你坚持调查，寻找调用跟踪中列出的其他函数可以帮助你缩小所需的 C 文件范围。但并无保证，而且这可能是

![](img/68d6731afe4338e918be0906dc327e1c_194_0.png)

图 6.3 Cscope 界面

Copyright ©Intel Corporation. All rights reserved.

# 第 6 章 深入技术

一个漫长而繁琐的过程。此外，每当你需要帮助时，只需按下 `?` 即可获得基础使用指南。此外，在内核源码目录中，你还可以运行 `cscope` 来创建 `cscope` 索引，以便以后更快搜索。

```
make cscope
```

## 反汇编对象

假设你已经找到了源代码，现在是反汇编由该源代码编译的对象了。首先，如果你运行的是调试内核，那么所有对象都已编译了调试符号。你很幸运。你只需要转储对象并深入到混合了的汇编-C 代码中。如果没有，你将必须使用调试符号重新编译源代码并对其进行逆向工程。
这不是一个简单或琐碎的任务。首先，如果你使用与编译原始文件不同的编译器，你的对象将与崩溃报告中的对象不同，这将使得你的努力变得困难，甚至不可能。

## 示例测试

我们称这个示例为简单示例，因为它与内核无关。它仅仅演示了如何编译对象然后对其进行反汇编。
运行 `make <object name>`。例如：

```
make object.o
```

# 崩溃分析 (crash) 187

请注意，如果没有指定需要执行操作的 Makefile，`make` 是没有意义的。但我们有一个 Makefile。它是我们在运行 `./configure` 之后创建的。否则，这一切将无法正常工作。Makefile 非常重要。我们很快就会看到一个不那么简单的示例。

如果你不删除对象，那么你可能无法编译它。Make 会比较源文件和对象的时间戳，除非你更改了源代码，否则对象的重新编译将失败。

现在，这里有另一个简单示例，注意创建的对象的大小差异，一个带有调试符号，另一个没有：

```
#gcc memhog.c -o memhog.no.symbols

#ls -l memhog.no.symbols

-rwxr-xr-x 1 iljubunc syseng 10417 2013-12-15 12:17 memhog.no.symbols

#gcc memhog.c -o memhog.symbols

#ls -l memhog.symbols

-rwxr-xr-x 1 iljubunc syseng 10417 2013-12-15 12:17 memhog.symbols
```
