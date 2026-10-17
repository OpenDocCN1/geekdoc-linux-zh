
单个选项`-a`在替换连续的两个或多个空格时插入制表符，并创建一个较小的输出文件。

另参见`expand`

## `unhash`

一个 C shell 内置命令，用于移除内部哈希表。在调用`unhash`之后，C shell 将停止使用哈希值来查找命令，并会花费更多时间搜索目录路径名。

另参见`hash`, `rehash`

## `uniq`

一个用于删除或报告排序后的文本文件中相邻重复行的命令。

### 语法

其使用语法如下：

```text
uniq [options][inputfile[outputfile]
```

`uniq`输入中的重复行除非它们是相邻的，否则不会被检测到，因此在使用`uniq`之前对文件进行排序也许是明智的。

### 选项和参数

`uniq`移除排序后的`inputfile`中的相邻重复行，将每行的一个副本发送到标准输出或`outputfile`。表 U.5 列出了你可以配合`uniq`使用的选项。

**表 U.5: 与 `uniq` 使用的选项**

| 选项 |  |
| --- | --- |
| `-c` | 在每行前面加上该行在输入中出现的次数。 |
| `-d` | 显示所有重复行（一次），但不显示唯一行。 |
| `-f n` | 忽略文件中的前 `n` 个字段及其之前的任何空格；并非所有 `uniq` 版本中都可用。 |
| `-s n` | 忽略前 `n` 个字符及其之前的任何空格；并非所有 `uniq` 版本中都可用。 |
| `-u` | 仅显示唯一行；不显示重复行。 |
| `-n` | 忽略文件中的前 `n` 个字段；此选项在某些 `uniq` 版本中已过时。 |
| `+n` | 忽略字段中的前 `n` 个字符；此选项在某些 `uniq` 版本中已过时。 |

## 第二十章

### 示例

`uniq`命令通常用作过滤器，擅长将两个文件合并产生一个删除所有重复项的输出文件。要将两个名称列表合并为一个不包含重复的列表，请使用：

```text
cat mylist yourlist | sort | uniq > ourlist
```

这使用`cat`命令合并`mylist`和`yourlist`，对结果进行排序，移除任何重复项，并将结果存储在文件`ourlist`中。

另参见`comm`, `sort`

## `units`

一个用于在不同计量单位之间转换的交互式程序。`units`程序只能进行乘法转换，因此它可以将温度从开尔文度转换为兰因度，但不能从华氏度转换为摄氏度。此外，许多货币汇率会波动，且可能不是最新的。以下是其工作原理的简短示例：

```text
+   - units
你有一个：inch
你想转换为：cm
* 2.54000e+00
/ 3.93701e-01
```

与美国对应部分不同的英国单位带有 `br` 前缀，例如：

```text
+   - brgallon
```

货币则为：

```text
+   - germanmark
```

或

```text
+   - britainpound
```

大多数熟悉的单位都能识别，包括公制前缀和缩写。要查看识别的约 500 个单位的完整列表，请查看 BSD 和 SunOS 系统上的 `/usr/share/units`，SVR4 上的 `/usr/lib/units`，SCO 上的 `/usr/lib/unitabb` 以及 Solaris 和 AIX 上的 `/usr/share/lib/unitabb`。

另参见`bc`, `dc`

## Unix

读音为 "yoo-nixs"。一种于 1969 年在 AT&T 贝尔实验室由 Ken Thompson 和 Dennis Ritchie 设计并开发的操作系统。自最初开发以来，Unix 环境已经通过大量的工具和其他程序变得日益丰富。真正的转折点是 1972 年到 1974 年期间，当时 Unix 用 C 语言重新编写，并以可移植性作为主要的设计目标。Unix 已经发展成为世界上使用得最广泛的通用型操作系统。表 U.6 列出了 Unix 和类 Unix 操作系统的名称及其开发者。

另参见 K&R

**表 U.6: Unix 系统及其开发者**

| UNIX 系统 | 开发者 |
| --- | --- |
| UNIX | AT&T 贝尔实验室 |
| BSD | Berkeley |
| AIX | IBM |
| Apple | Apple |
| FreeBSD | 卡内基梅隆大学 |
| Mach | Andrew Tanbaum |
| Minix | Sequent Systems |
| NeXT | NeXT |
| OSF | Software Foundation |
| HP-UX | 惠尔-包罗 |
| Irix | Silicon Graphics |
| Linux | Linus Torvalds |
| NetBSD | 自由软件 |
| Windows NT | Microsoft |
| OpenBSD | OpenBSD |
| SCO | Santa Cruz |
| Solaris | Sun Microsystems |
| SunOS | Sun Microsystems |
| TrueBSD |  |
| Vanium | Microsoft |
| Ultrix | Digital Corporation |
| Ultrix | Digital Corporation |
| UnixWare | Novell/Santa Cruz |
| Unicos | Cray Research |

## `unlimit`

一个移除资源的命令。它被用于撤销任何限制，语法为：

```text
unlimit [resources]
```

其中`resources`是表 U.7 中的一个。如果你不指定`resources`，则移除所有限制。

另参见`limit`

**表 U.7: 与之一起使用的资源名称**

| 资源 | 描述 |
| --- | --- |
| `Cptime` | 最大处理器秒数 |
| `Filesize` | 任何文件的最大大小 |
| `Datasize` | 数据最大大小（包括栈） |
| `Stacksize` | 栈的最大大小 |
| `Coredumpsize` | 转储的最大大小 |

## `unpack`

一个展开由`pack`压缩文件的命令。语法为：

```text
unpack file-list
```

其中`file-list`包含你想要解压缩的文件名。所有此类文件的扩展名为`.z`；假设你不需要在命令行中指定它。

另参见`compact`, `compress`, `gzip`, `pack`, `pcat`, `uncompress`, `zcat`

## `unset`

一个内置命令，用于移除一个或多个变量。Bourne shell 的语法为：

```text
unset names
```

其中`names`指定你想移除的变量。

在 Korn shell 中，函数必须显式使用`-f`选项，例如：

```text
unset f names
```

如果要关闭 shell，可以使用文件名元字符指定变量名。在 C shell 中，你也可以通过设置它们的反值来取消 C 变量。

另参见`set`, `setenv`, `unset`

## `unsetenv`

一个 C shell 内置命令，用于移除环境变量。语法为：

```text
unsetenv name
```

其中`name`代表你想移除的变量。你不能使用文件名元字符指定环境变量。

另参见`set`, `setenv`, `unset`

## `until`

Bourne shell 和 Korn shell 的编程结构，通常用于`test`设置循环。只要结果为假（返回非零值），循环就会继续运行。当返回真值时，循环终止。一个示例可能如下：

```text
until condition
do
  commands
done
```

另参见`do`, `done`, `fi`, `for`, `if`, `then`, `until`, `while`

## `unvis`

一个 BSD 命令，用于撤销`vis`命令的效果，并将非打印字符转换回原始形式。

另参见`vis`

## `uptime`

一个通过显示当前时间、系统运行时间以及数量来显示系统运行多久的命令。

当前登录的用户，以及过去一、五、十五分钟的系统负载平均值。

**另见**`uptime`, `w`, `who`

## URL

统一资源定位符（Uniform Resource Locator）的缩写，读音为 "earl"。一种访问互联网资源的方法。

URL 包含了有关要使用的访问方法以及资源本身的信息。Web 浏览器使用 URL 来直接连接到万维网上的特定文档或页面，而无需您知道该资源的物理位置。一个示例 URL 可能看起来如下所示：

```text
http://www.austin.ibm.com
```

URL 的第一部分（冒号之前）指定了访问方法。在 Web 终端中，这通常是`http`（代表超文本传输协议），但您也可能会看到`file`、`ftp`或`gopher`。URL 的第二部分（冒号之后）指定了资源。双斜杠之后的文本通常表示服务器名称，而单斜杠之后的文本定义了您将要连接的目录或单个文件。如果您链接到一个文档，它通常具有文件扩展名`.html`，这是 "超文本标记语言"（Hypertext Markup Language）的缩写。

URL 总是区分大小写的，因此请特别注意大写和小写字母以及符号。

## `users`
