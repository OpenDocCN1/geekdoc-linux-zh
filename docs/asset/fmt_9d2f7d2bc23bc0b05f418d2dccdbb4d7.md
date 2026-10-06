
`drwxr-xr-x 2 ftp ftp 2048 Jul 19 10:11 .`

`drwxr-xr-x 12 ftp ftp 1024 Jul 16 13:58 ..`

`n---r--r-- 1 ftp ftp 71801 Jul 19 10:11 yard-1.6.tar.gz`

`---r--r-- 1 ftp ftp 611342 Jul 19 10:11 zsh-3.0-pre3.tgz`

```
```bash
226 Transfer complete.
ftp> get yard-1.6.tar.gz src/yard-1.6.tar.gz
200 PORT command successful.
150 Opening BINARY mode data connection for yard.tar.gz (71801 bytes).
226 Transfer complete.
71801 bytes sent in 0.455 secs (1.52e+02 Kbytes)
ftp> !
->ls
```
```

```
```bash
379a.txt 381a.txt 383.txt
-> ^A
ftp> cd ../incoming
250 CWD command successful.
ftp> prompt
Interactive mode off.
ftp> mput *.txt
local: ./379a.txt remote: ./379a.txt
200 PORT command successful.
150 Opening BINARY mode data connection for ./379a.txt.
226 Transfer complete.
442 bytes sent in 0.0608 secs (6.2 Kbytes/sec)
local: ./381a.txt remote: ./381a.txt
200 PORT command successful.
150 Opening BINARY mode data connection for ./381a.txt.
226 Transfer complete.
285 bytes sent in 0.0319 secs (8.7 Kbytes/sec)
local: ./383.txt remote: ./383.txt
200 PORT command successful.
150 Opening BINARY mode data connection for ./383.txt.
226 Transfer complete.
1071 bytes sent in 0.00201 secs (5.2e+02 Kbytes/sec)
ftp> quit
221 Goodbye.
```
```

更多信息请参阅第 169 页和 918 页。

## Syntax

更多信息请参阅第 169 页和 918 页。

## Arguments

更多信息请参阅第 169 页和 918 页。

## Options

更多信息请参阅第 169 页和 918 页。

| 扩展名 | 含义 |
| :--- | :--- |
| `.c` | C 语言源码 |
| `.C`, `.cc`, `.cxx` | C++ 语言源码 |
| `.i` | 预处理 C 源 |
| `.ii` | 预处理后的 C++ 源 |
| `.s` | 汇编语言文件 |
| `.S` | 汇编语言文件 |
| `.0` | 目标文件 |
| `.a` | 模块库 |

## gcc 749

它们在命令行上出现的顺序。链接器仅使用库来解析来自命令行中该库选项之前的模块的未定义符号。你可以使用之前显示的 `-L` 选项添加其他库来搜索 `liburg.a`。

## -Wall

使 `gcc` 对 C 和 C++ 源文件中的可疑代码发出警告。有许多相关选项可以更精确地控制警告信息。（参见 GNU C 文档。）

## -pedantic

GNU 编译器接受的 C 语言包含了不属于 ANSI C 语言标准的特性。使用这些语言扩展，并仅接受 C 编程语言特征。

## -traditional

使 `gcc` 仅接受传统的 Kernan 和 Ritchie C 编程语言中提供的 C 编程语言特征。此选项允许你正确编译使用 ANSI C 语言定义之前的传统的 C 语言编写的旧程序。

## -D=[value]

通常 `#define` 预处理器指令在头文件或包含文件中给出。你可以使用它在命令行上定义符号名称。例如，`-DLux` 等同于在包含文件中有一行 `#define Linux`，而 `-DMCH=i586` 等同于 `#define MACH i586`。

## -fpic

使 `gcc` 生成位置无关代码，适用于安装到共享库中。

## -fwritable-strings

默认情况下，GNU 编译器将字符串常量放入受保护的内存中，在那里无法被修改。通常（某些旧的）程序假设你可以修改字符串常量。此选项更改 `gcc` 的行为，使得字符串常量可以被修改。

## Notes

上述选项列表只是 GNU 编译器可用完整选项集的一小部分。请查看 `gcc` man 页面获取完整列表。

虽然 `-o` 选项通常用于指定存储对象代码的文件，但此选项也可以用于命名其他编译步骤产生的文件。在下面的示例中，`-o` 选项导致后续 `gcc` 命令产生的汇编语言存储在文件 `acode` 中而不是 `pgm.s`，

```
$ gcc -S -o acode pgm.c
```

UNIX 系统中的 `lint` 工具在 Linux 上不可用。但是，`-Wall` 选项执行许多相同的检查，可以代替 `lint` 使用。

## 750 gcc

## Examples

第一个示例编译、汇编并链接了单个 C 程序 `compute.c`。可执行输出被放在 `a.out` 中。`gcc` 工具删除了对象文件。

```
$ gcc compute.c
```

下一个示例使用 C 优化器选项 `-O` 编译同一个程序。它先汇编然后链接优化后的代码。`-o` 选项导致 `gcc` 将可执行输出放在 `compute` 中。

```
$ gcc -o compute compute.c
```

接下来，编译、汇编并链接了一个 C 源文件、一个汇编语言文件和一个对象文件。可执行输出到 `progo`。

```
$ gcc -o progo.procom.profast.sprout.o
```

在下一个示例中，`gcc` 在链接 `him` 程序时会搜索存储在 `/lib/libm.a` 的标准数学库。它将可执行输出放在 `a.out` 中。

```
$ gcc him.c -lm
```

在最后一个示例中，C 编译器使用选项编译 `topo.c`，这些选项检查代码中的可疑源实践（`-Wall`）和违反 ANSI C 标准的行为（`-pedantic`）。`-g` 选项在可执行执行文件中启用调试支持，该文件通过 `-o topo` 选项保存为 `topo`。通过 `-O3` 选项启用完全优化。

C 编译器产生的警告显示在标准输出上。在这个示例中，第一个和最后一个警告来自 `-pedantic` 选项。其他警告源于 `-Wall` 选项。

```
$ gcc -Wall -g -O3 -pedantic -o topo topo.c
In file included from topo.c:2
/usr/include/ctype.h:65: warning, comma at end of enumerator list
topo.c:13: warning: return-type defaults to 'int'
topo.c: In function 'main'
topo.c:14: warning: unused variable 'c'
topo.c: In function 'getline'
topo.c:44: warning: 'c' might be uninitialized in this function
```

在编译使用 X11 包含文件和库程序时，你可能需要使用 `-I` 和 `-L` 选项告诉 `gcc` 在哪里定位这些文件和库。下一个示例使用了这些选项，并指示 `gcc` 用基础 X11 库链接程序：

```
$ gcc -I/usr/X11R6/include plot.c -L/usr/X11R6/lib -l11
```

## grep 在文件中搜索模式

| 语法 |
| --- |
| `grep [options] pattern [file-list]` |

## Summary

`grep` 逐行搜索一个或多个文件中的匹配模式。模式可以是简单的字符串，也可以另一种形式的正则表达式（关于正则表达式的更多信息请参见附录 A）。每当 `grep` 找到包含模式匹配项的行时，都会执行由选项指定的各种操作。

`grep` 工具从你在命令行上指定的文件或标准输入获取输入。

## Arguments

模式是一个正则表达式，如附录 A 所定义。你必须对包含特殊字符、空格（SPACES）或制表符（TABS）的正则表达式加引号。引用这些字符的一种简单方法是将整个表达式括在单引号内。

`file-list` 包含 `grep` 搜索的普通文本文件的路径名。

## Options

如果你不指定任何选项，`grep` 将包含匹配项的行发送到标准输出。如果指定了多个文件，`grep` 会在每行前加上文件名。

## Major Options

你一次只能使用以下选项中的一个。

- `-G` 将模式解释为正则表达式。如果未指定，这是默认选项。
- `-E` 将模式解释为扩展正则表达式。命令 `grep -E` 类似于 `grep`。
- `-F` 将模式解释为固定字符串。命令 `grep -F` 等于 `grep`。

## Other Options

- `-c` 显示每个文件中包含匹配项的行数。
- `-h` 如果给了多个文件，输出时不加文件名。
- `-i` 忽略模式中的小写以匹配文件中的大写，反之亦然。
- `-l` 列出包含一个或多个匹配的文件名。即使文件包含多个匹配项，也只显示一次。
- `-n` 显示文件中每行的行号。文件不需要包含数字。此数字代表从文件中到显示行的行数。
- `-q` 静默不向 stdout 发任何内容；仅设置退出码。
- `-s` 如果 `file-list` 中的文件不存在或不可读，不显示错误消息。
- `-v` 反向测试使不包含匹配项的行满足搜索。当你单独使用此选项时，`grep` 显示所有不包含模式匹配的行。
- `-w` 使用此选项，模式必须匹配整个单词。如果你正在搜索一个可能作为文件中另一个单词子字符串出现的单词，这非常有帮助。

## Notes

`grep` 在找到匹配时返回退出状态 0，未找到匹配返回 1，如果文件不可访问或存在语法错误返回 2。

有两个工具执行与 `grep` 类似的功能。`eg` 工具（类似于 `grep -E`）允许你使用扩展正则表达式，它比基础正则表达式包含一组不同的特殊字符（第 911 页）。`fg` 工具（同于 `grep -F`）速度快且紧凑，但只处理简单字符串。

## Examples

以下示例假设工作目录包含三个文件：`testa`、`testb` 和 `testc`。每个文件的内容为

| Filea | Fileb | Filec |
|---|---|---|
| aaab | aaaaa | AAAAA |
| bbbcc | bbbbb | BBBBB |
| ff-cd | ccccc | CCCC |
| ccccd | ddddd | DDDDD |
| dddaa | | |

`grep` 工具可以搜索简单字符字符串的模式。以下命令搜索 `testa` 并显示包含字符串 `bb` 的每一行：

```bash
$ grep bb testa
aaabb
bbbcc
```

`-v` 选项会反转测试结果。下面的示例显示了所有不包含 `bb` 的行：

```bash
$ grep -v bb testa
ffff
cccd
dddaa
```

`-n` 选项显示每个输出行的行号。

```bash
$ grep -n bb testa
1:aaabb
2:bbcc
```

`grep` 实用程序可以搜索多个文件。在这里，`grep` 搜索工作目录下的每个文件。（歧义的文件引用 `*` 匹配所有文件名。）包含该字符串的文件名会显示在每行内容的之前：

```bash
$ grep bb *
testa:aaabb
testa:bbcc
testb:bbbb
```

当使用 `-w` 选项对字符串 `bb` 进行搜索时，`grep` 不产生输出，因为没有一个文件将 `bb` 作为一个独立的单词出现。

```bash
$ grep -w bb *
$
```

`grep` 执行的搜索是区分大小写的。由于之前的示例指定了小写的 `bb`，因此 `grep` 没在 `testc` 中找到大写的字符串 `BBBB`。`-i` 选项会模式模式中的字母匹配大写或小写。

```bash
$ grep -i bb *
testa:aaabb
testa:bbcc
testb:bbbb
testc:BBBB
```

```bash
$ grep -i BB *
testa:aaabb
testa:bbcc
testb:bbbb
testc:BBBB
```

`-c` 选项显示每个文件中包含匹配项的行数。

```bash
$ grep -c bb *
testa:2
testb:1
testc:0
```

# 754 grep

下面的命令行显示了来自文件 `text2` 的包含以 `st` 开头的字符串的行，后面跟了零或多个字符（`.*` 在正则表达式中表示零或多个字符——见附录 A），并以 `ing` 结尾。

```bash
$ grep 'st.*ing' text2
.\.
```

正则表达式 `^` 匹配行的开头，它可以单独使用来匹配文件中的每一行。与 `-n` 选项配合使用，它可以显示文件中的行，并在其前面加上行号。

```bash
$ grep -n '^' testa
1:aaabb
2:bbbcc
3:ffff
4:cccd
5:ddaa
```

下一个命令行计算了工作目录中 C 源码中 `#include` 语句出现的次数。`-h` 选项导致 `grep` 在输出中抑制文件名。`sort` 的输入是来自 `*.c` 的所有匹配 `#include` 的行。`sort` 的输出是一个经过排序的行列表，其中包含许多重复项。使用带有 `-c` 选项的 `uniq` 处理此列表，它只会输出一次重复的行，并输出其重复的次数。

```bash
$ grep -h '^include' *.c | sort | uniq -c
9 #include "buff.h"
2 #include "screen.h"
1 #include "poly.h"
6 #include "window.h"
2 #include "x2.h"
2 #include "x3.h"
2 #include <math.h>
3 #include <stdio.h>
```

最后的命令行调用 `vi` 编辑器编辑工作目录中包含字符串 `Sampson` 的文件列表。反引号（第 327 页）导致 shell 原地地执行 `grep` 命令，并为 `vi` 提供你想要编辑的文件名列表。（在本例中，单引号不是必须的，但如果你搜索的字符串包含特殊字符或空格，则是必须的。通常的好习惯是给模式加引号，以免 shell 解析其中可能包含的特殊字符。）

```bash
$ vi `grep -1 'Sampson' *`
.
```
