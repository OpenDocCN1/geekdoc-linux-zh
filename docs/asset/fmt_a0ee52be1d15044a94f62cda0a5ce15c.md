
gawk [ POSIX or GNU style options ] [ -- ]program-text file ...

```
gawk 是 GNU 项目对 awk 编程语言的实现。它符合 POSIX 1003.2 命令语言和实用程序标准中对该语言的定义。此版本又基于 Aho、Kernighan 和 Weinberger 所著《The AWK Programming Language》中的描述，并具有在 UNIX awk 的 System V Release 4 版本中发现的附加功能。`gawk` 还提供更新的 Bell Labs awk 扩展以及一些 GNU 特定扩展。

## gcc, g++—GNU project C and C++ Compiler (v2.7)

```
gcc [ option | filename ]...
g++ [ option | filename ]...
```

## getopt(s)—parses command-line options

`getopts` 命令取代了 `getopt`。`getopts` 用于将命令行中的选项分解以便 shell 过程易于解析，并检查选项是否合法。

## grep—searches a file for a pattern

```
grep [ -bchilnsvw ] limited-regular-expression [ filename ... ]
```

`grep` 在文件中搜索模式并打印包含该模式的所有行。使用正则表达式元字符来匹配模式。`egrep` 具有扩展的元字符集。

## EXAMPLE A.32

```
1  grep Tom file1 file2 file3
2  grep -in 'Atom savage' *
```

# 说明

+   1. `Grep` 显示 `file1`、`file2` 和 `file3` 中包含模式 `Tom` 的所有行。
+   2. `Grep` 显示当前工作目录中包含 `Tom` 的文件中的所有行，并显示行号，如果它出现在行的开头，则保存到 stdout，忽略大小写。

## groups—打印用户所属的组

```
groups [ user... ]
```

命令 `groups` 在标准输出上打印你或可选指定的用户所属的组。

## gzip, gunzip, zcat—压缩或扩展文件

```
gzip [ -acdfhlLnNrtVv19 ] [-S suffix] [ name ... ]
gunzip [ -acdfhlLnNrtVv ] [-S suffix] [ name ... ]
zcat [ -fhLV ] [ name ... ]
```

`gzip` 使用 Lempel-Ziv 编码（LZ77）减小命名文件的大小。每当可能时，每个文件都会被替换为扩展名为 `.GZ` 的文件，同时保持相同的拥有者模式、访问权限和修改时间。

## head—输出文件的前十行

```
head [-c N[k|m]] [-n N] [-qv] [bytes=N[k|m]] [ -lines=N] [--quiet]
[--silent] [--verbose] [--help] [--version] [file...]
head [-N[k|m]qv] [file...]
```

`head` 将每个文件的前十行显示到标准输出。文件多于一个时，它会在每个文件前加上一个包含文件名的标题。没有文件或文件为 `-` 时，读取标准输入。

## host—打印 DNS 中指定主机或区域的信息

```
host [] [-v] [-w] [-r] [-d] [-t querytype] [a] host [server]
```

`host` 命令打印有关指定 Internet 主机的信息。它从遍布全国的互联服务器集中获取信息。默认情况下，它在主机名和 IP 地址之间转换。使用 `-a` 或 `-t` 开关时，会打印所有信息。

## id—打印用户名、用户 ID、组名和组 ID

```
/usr/bin/id [-a]
```

`id` 显示你的用户 ID、用户名、组 ID 和组名。如果你的真实 ID 和有效 ID 不匹配，则两者都会打印。

## jsh—标准作业控制 shell

```
jsh [ -acefhiknprstuvx ] [ argument... ]
```

命令 `jsh` 是标准 Bourne shell 的接口，提供 Bourne shell 的所有功能并启用作业控制。

## kill—发送信号以终止一个或多个进程

```
kill [
```

`kill` 发送信号以终止一个或多个进程 ID。

## killall—按名称杀死进程

## less—more 的相反操作

```
less -?
less --help
less -V
less --version
less [-+][aAbBcCdDeEfFgGiImMnNoOqQrRsSuUuWwXx][-b bufs] [-h lines] [-j line] [-k keyfile][-o[0] logfile] [-p pattern] [-P prompt] [-t tag] [-T tagsfile] [-x tab] [-y lines] [-[z] lines] [+{+cmd}] [--] [filename]...
```

`less` 是一个类似于 `more` 的程序，但允许在文件中向后移动以及向前移动。此外，`less` 在开始之前不必读取整个输入文件，因此对于大型输入文件，其启动速度比 `vi` 等文本编辑器更快。`less` 使用 `termcap`（某些系统上使用 `terminfo`），因此可以在各种终端上运行。甚至对硬拷贝终端也有有限的支持。

## line—读取一行

`line` 从标准输入复制一行（直到换行符）并将其写入标准输出。它在 EOF 时返回退出代码 1，并且始终至少打印一个换行符。它通常在 shell 文件中用于从用户终端读取。

如果最后一个参数命名的是现有目录，`ln` 将每个其他给定文件链接到该目录中同名文件。如果只给出一个文件，它会将该文件链接到当前目录。否则，如果只给出两个文件，它会将第一个文件链接到第二个文件。如果最后一个参数不是目录且给出超过两个文件，则为错误。跨分区时使用符号链接。

## 选项：

| 选项 | 描述 |
|---|---|
| `-b, --backup` | 对即将被删除的文件进行备份。 |
| `-d, -F, --directory` | 允许超级用户对目录进行硬链接。 |
| `-f, --force` | 删除已存在的目标文件。 |
| `-i, --interactive` | 提示是否删除已存在的目标文件。 |
| `-n, --no-dereference` | 当指定的目标是目录的符号链接时，尝试替换符号链接而不是将其解析为在指向的目录中创建链接。此选项与 `--force` 结合使用时最有用。 |
| `-s, --symbolic` | 创建符号链接而不是硬链接。 |
| `-v, --verbose` | 在链接文件之前打印每个文件的名称。 |
| `--help` | 在标准输出上打印使用消息；成功退出。 |
| `--version` | 在标准输出上打印版本信息；成功退出。 |
| `-S, --suffix backup-suffix` | 用于创建简单备份文件的后缀可以使用 `SIMPLE_BACKUP_SUFFIX` 环境变量设置，该变量可被此选项覆盖。如果两者均未给出，则默认为 `~`，与 `emacs` 相同。 |
| `-V, --version-control {numbered,existing,simple}` | 所做的备份类型可以使用 `VERSION_CONTROL` 环境变量设置。 |

## 示例 43

```
1  % ls -l
   total 2
   drwxrwsr-x  2 ellie  root  1024 Jan 19 18:34 dir
   -rw-rw-r--  1 ellie  root    16 Jan 19 18:34 filex
2  % ln filex dir
3  % cd dir
4  % ls -l
   total 1
   -rw-rw-r--  2 ellie  root    16 Jan 19 18:34 filex
```
