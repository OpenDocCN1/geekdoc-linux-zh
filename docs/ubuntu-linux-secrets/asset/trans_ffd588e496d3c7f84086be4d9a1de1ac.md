

表 27-5：objdump 参数

| 参数 | 描述 |
|---|---|
| -a | 如果有任何文件是归档文件，则显示归档头信息 |
| -b | 指定目标代码文件的目标代码格式 |
| -C | 将低级符号解混淆为用户级名称 |
| -d | 将目标代码反汇编为指令代码 |
| -D | 将所有节反汇编为指令代码，包括数据 |
| -EB | 指定大端目标文件 |
| -EL | 指定小端目标文件 |
| -f | 显示每个文件的头中的摘要信息 |
| -G | 显示调试节的内容 |
| -h | 显示每个文件的节头中的摘要信息 |
| -i | 显示所有架构和目标格式的列表 |
| -j | 仅显示指定节的信息 |
| -l | 用源代码行号标记输出 |
| -m | 指定反汇编时使用的架构 |
| -p | 显示特定于目标文件格式的信息 |
| -r | 显示文件中的重定位条目 |
| -R | 显示文件中的动态重定位条目 |
| -s | 显示指定节的完整内容 |
| -$ | 显示与反汇编代码混合的源代码 |
| -t | 显示文件的符号表条目 |
| -T | 显示文件的动态符号表条目 |
| -x | 显示文件的全部可用头信息 |
| --start-address | 从指定地址开始显示数据 |
| --stop-address | 在指定地址停止显示数据 |

objdump 程序是一个非常通用的工具。它可以解码除目标代码文件之外的许多不同类型的二进制文件。对于 C 程序员来说，-d 参数是最有用的，因为它显示反汇编的目标代码文件。

## 一个 objdump 示例

使用示例 C 程序，你可以通过使用 -c 选项编译程序来创建一个要转储的目标文件：

```
$ gcc -c ctest.c
```

这会创建一个 *object file*。目标文件包含程序生成的原始汇编语言代码，在链接成系统应用程序文件之前。此时你可以使用 `objdump` 程序来查看 C 程序生成的原始汇编语言代码：

```
```text
$ objdump -d ctest.o

ctest.o: file format elf32-i386

Disassembly of section .text:

00000000 <main>:
0: 8d 4c 24 04 lea 0x4(%esp),%ecx
4: 83 e4 f0 and $0xfffffff0,%esp
7: ff 71 fc pushl -0x4(%ecx)
a: 55 push %ebp
b: 89 e5 mov %esp,%ebp
d: 51 push %ecx
e: 83 ec 04 sub $0x4,%esp
11: c7 04 24 00 00 00 00 movl $0x0,(%esp)
18: e8 fc ff ff ff call 19 <main+0x19>
1d: b8 00 00 00 00 mov $0x0,%eax
22: 83 c4 04 add $0x4,%esp
25: 59 pop %ecx
26: 5d pop %ebp
27: 8d 61 fc lea -0x4(%ecx),%esp
2a: c3 ret
$ 
```
```

反汇编的目标代码文件显示了编译器创建的汇编语言助记符以及对应的指令代码。你可能会注意到，程序中引用的内存地址被清零了。这些值要等到链接器链接应用程序并准备好在系统上执行时才会确定。在此步骤中，你可以轻松看到执行这些功能的指令。

## GNU 分析器程序

GNU 分析器 (`gprof`) 是包含在 `binutils` 包中的另一个程序。该程序用于分析程序执行并确定应用程序中的“热点”。

应用程序热点是程序运行时需要最多处理时间的函数。它们通常是最数学密集的函数，但并非总是如此。I/O 密集型函数也会增加处理时间。

本节描述 GNU 分析器并演示如何在 C 程序中使用它来查看不同函数在应用程序中消耗了多少时间。

## 使用分析器

与其他工具一样，gprof 是一个命令行程序，使用多个参数来控制其行为。gprof 的命令行格式为

```
gprof [ -[abcDhilIsTvwxyz] ] [ -[ACEeFfJjnNdpQqZ][name] ]
[ -i dirs ] [ -d [num] ] [ -k from/to ]
[ -m min-count ] [ -t table-length ]
[ --[no-]annotated-source[name] ]
[ --[no-]exec-counts[name] ]
[ --[no-]flat-profile[name] ] [ --[no-]graph[name] ]
[ --[no-]time-name ] [ --all-lines ] [ --brief ]
[ --debug[level] ] [ --function-ordering ]
[ --file-ordering ] [ --directory-path-dirs ]
[ --display-unused-functions ] [ --file-format=name ]
[ --file-info ] [ --help ] [ --line ] [ --min-count=n ]
[ --no-static ] [ --print-path ] [ --separate-files ]
[ --static-call-graph ] [ --sum ] [ --table-length=len ]
[ --traditional ] [ --version ] [ --width=n ]
[ --ignore-non-functions ] [ --demangle=STYLE ]
[ --no-demangle ] [ image-file ] [ profile-file... ]
```

这组参数字母汤分为三组：

- ◆ 输出格式参数
- ◆ 分析参数
- ◆ 杂项参数

输出格式选项允许你修改 gprof 的输出。这些选项在表 27-6 中显示。

## 表 27-6：gprof 输出格式选项

| 参数 | 描述 |
|-----------|-------------|
| -A | 显示所有函数或仅指定函数的源代码 |
| -b | 不显示解释分析字段的详细输出 |
| -C | 显示所有函数或仅指定函数的总汇总 |
| -i | 显示配置文件数据的摘要信息 |
| -I | 指定查找源文件的搜索目录列表 |
| -J | 不显示带注释的源代码 |
| -L | 显示源文件名的完整路径 |
| -p | 显示所有函数或仅指定函数的平面分析 |
| -P | 抑制所有函数或仅指定函数的平面分析打印 |

