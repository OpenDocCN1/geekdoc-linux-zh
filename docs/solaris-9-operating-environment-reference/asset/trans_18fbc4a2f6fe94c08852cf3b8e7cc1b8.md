
该顺序意味着 LANG 的新设置并不会覆盖 LC_CTYPE 的设置。当所有值均无效时，字符分类默认为 POSIX.1 C 语言环境。

## 属性

请参见 attributes(5)以获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可性 | SUNWcsu |

## 参见

localedef(1), attributes(5)

## dumpkeys — 转储键盘翻译表

## 摘要

/usr/bin/dumpkeys

## 描述

参见 loadkeys(1)。

## echo — 将参数写入标准输出

## 摘要

/usr/bin/echo [string...]
/usr/ucb/echo [-n] [string...]

## 描述

echo 命令将其以空格分隔并以换行符结束的参数写入标准输出。如果你没有提供任何参数，则只写入换行符。

echo 用于在命令行文件中生成诊断信息、向管道发送已知数据以及显示环境变量的内容。

C shell、Korn shell 和 Bourne shell 都有内置命令，默认情况下，如果你在不带完整路径的情况下调用 echo，则会调用这些命令。参见 shell-builtins(1)。

sh echo、ksh echo 和 /usr/bin/echo 命令理解反斜杠转义字符，但 sh echo 命令不理解 \a 为警报字符。此外，ksh echo 命令没有 -n 选项。sh echo 和 /usr/bin/echo 只有在设置了 SYS3 环境变量时才有 -n 选项。如果设置了该变量，上述提到的所有反斜杠字符均不可用。相反，csh echo 和 /usr/ucb/echo 命令具有 -n 选项，但不理解反斜杠转义字符。

## echo

## 选项

/usr/ucb/echo
-n 不向输出中添加换行符。

> 注意 — 提供 n 选项是为了 BSD 应用程序的过渡，在未来的发布中可能不再受支持。

## 操作数

string 一个要写入标准输出的字符串。如果任何操作数是 -n，则它被视为字符串而非选项。

/usr/bin/echo
在任何参数中均可识别以下字符序列：

- \a 警报字符。
- \b 退格符。
- \c 打印行但不加换行符。
- \f 换页。
- \n 换行符。
- \r 回车。
- \t 制表符。
- \v 垂直制表符。
- \ll 反斜杠。
- \0n 其中 n 是 8 字节字符，其 ASCII 是表示该字符的 1、2 或 3 位八进制数。

当使用转义约定 \0n 表示 8 字节字符时，n 必须始终跟在数字零 (0) 后面。
例如，以下命令打印短 WARNING: 并在终端上响铃。

```
$ echo 'WARNING:\007 '
WARNING:
$
```

需要单引号（或双引号）（或两个反斜杠）来保护位于 07 之前的反斜杠。
在 \0 之后，你可以使用最多三个数字来构造输出字符。如果在 \0n 之后，你想 echo 不属于八进制表示的额外数字，你必须使用完整的 3 位 n。例如，如果你想 echo ESC 7，必须使用三个数字 033，而不是仅在 \0 之后使用两个数字 33。
此示例表明仅在后面使用两个数字是错误的。

```
$ echo "0337" | od -xc
000000 df0a
337 \n
000002 $
```

## echo

以下示例显示 3 位语法可产生正确的结果。
$ echo "\00337" | od -xc
000000 0000 0337 \n
000002 $

对于每个字符的八进制序列，请参见 ascii(5)。

## 使用

可移植应用程序不应使用 -n（作为第一个参数）或转义序列。可以使用 printf(1) 命令可移植地模拟 echo 命令的任何传统行为，如下：

Solaris /usr/bin/echo 等同于：
printf "%b\n" "$*"

/usr/ucb/echo 等同于：
if [ "$1" = "-n" ];
then
  shift
  printf "%s" "$*"
else
  printf "%s\n" "$*"
fi

鼓励新应用程序使用 printf 代替 echo。

## 示例

你可以使用 echo 命令通过在变量名前加上美元符号 ($) 来显示变量的值。以下示例显示 PATH 环境变量的值。

```
$ echo $PATH
/usr/bin:/bin:/sbin:/etc:/opt/bin:/local/games
```

以下示例显示了如何将 echo 命令与 tr 和 wc 命令结合使用，确定 / 和当前目录之间有多少个子目录。该示例包含以下部分：

- Echo 工作目录的完整路径。
- 将输出通过管道 tr 将路径中嵌入的斜杠转换为空格字符。
- 将输出通过管道 wc -w 统计路径中的名称。

```
$ echo / | tr '/' ' ' | wc -w
```

请参见 tr(1) 和 wc(1) 其功能。

以下示例显示了不带换行符的 echo 字符串的不同方法。

```
/usr/bin/echo "$USER's current directory is $PWD"
```

以下示例显示了不带换行符的 echo 字符串的不同方法。

```
/usr/bin/echo "$USER's current directory is $PWD"
```

## Bourne and Korn Shell

```
$ /usr/bin/echo "$USER's current directory is $PWD"
```

## C Shell

```
$ /usr/bin/echo -n "$USER's current directory is $PWD"
```

## 环境变量

SYSV3 提供了与 INTERACTIVE UNIX 安装脚本的兼容性。SYSV3 仅用于兼容性，不应在新脚本中使用。参见 environ(5)以获取影响影响 echo 执行的变量描述：LC_TYPE、LC_MESSAGES 和 PATH。

## 退出状态

- 0 成功完成。
- 1 发生错误

## 属性

请参见 attributes(5)以获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可性 | SUNwcsu |

| 属性类型 | 属性值 |
| :--- | :--- |
| 可性 | SUNwcpu |

## 参见

printf(1), shell-builtins(1), tr(1), wc(1), echo(1), attributes(5), environ(5)

## ed, red — 文本编辑器

## 摘要

```
/usr/bin/ed [-s] [-p string] [-x] [file]
/usr/bin/ed [-s] [-p string] [-x] [file]
/usr/bin/ed [-s] [-p string] [-x] [file]
```

## 描述

ed 是标准的文本编辑器。如果你指定一个文件，ed 会将文件读入 ed 的缓冲区，以便进行编辑。

> 注意 — 尽管我们已经取代了 ed 作为行编辑器，但 diff 等命令继续使用 ed。

ed 命令在它正在编辑的文件副本上操作；在使用写入命令之前，原始文件保持不变。编辑后的文本副本保存在一个名为 buffer 的临时文件中。只有一个缓冲区。

与 vi 和 ex 命令不同，除非你要求，否则 ed 不显示其缓冲区中的任何文本。因此，要跟踪缓冲区的内容是困难的。

red 限制为标准 ed。它只允许编辑当前目录下的文件。它禁止使用 ! 命令执行 shell 命令。尝试绕这些限制会导致错误消息（受限 shell）。

ed 和 red 都支持 spec(4) 格式功能。默认模式是 stty 制表符或 stty，即制表符在八列处停止（参见 stty(1)）。然而，如果文件的第一行包含格式规范，该规范将覆盖默认模式。以下文件第一行的示例在 5,10 和 15 处停止，最大长度为 72。

```
<t:5,10,15>:
```

ed 命令具有简单规则的结构：零、一个或两个地址后跟着单字符命令，可能还跟着该命令的参数。地址指定缓冲区中的一个或多个。每个命令都需要默认地址，因此你通常可以省略地址。通常每行只能指定一个命令。

ed 有独立的输入模式。某些命令允许输入文本。这被放在缓冲区适当的位置。当 ed 接受文本时，ed 不识别任何命令；它仅仅收集所有输入。通过在行开头输入一个点 (.) 紧接着按回车即可离开输入模式。

> 注意 — 如果编辑器来自命令文件（例如，ed file < ed-cmd-file），编辑器会在第一次失败时退出。

ed 有以下大小限制：

