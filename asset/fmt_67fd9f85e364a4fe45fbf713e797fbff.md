
# 正则表达式

正则表达式可以非常简单，也可以非常复杂，取决于它们所使用的程序以及你正在寻找的内容。它们可以包含元字符或普通字符。正则表达式是用于匹配某些内容的语法，而元字符允许你用较小的预定义字符子集来扩展更复杂的普通字符组。下面的正则表达式是一个非常简单的表达式，它可以匹配括号内的任意单个字符：

```
c[a-n]n
```

正则表达式可以像下面这样复杂：

```
[0-9][0-9][0-9]\[[0-9][0-9][0-9]\\[[0-9][0-9][0-9]
```

这将匹配美国电话号码的标准格式（例如，555.555.0000）。注意，`\`（反斜杠）转义了`.`（点），使得点号表示字面上的点，而不是点号元字符通常表示的意思（一个或多个字符）。

学习使用正则表达式和元字符可能是一个漫长而复杂的过程，但理解这些基础将帮助你完成 Unix 系统上所需的操作。对正则表达式的全面讨论超出了本书的范围，但 Andrew Watt 编写的《Beginning Regular Expressions》（Wiley, ISBN 0-7645-7489-2）是深入学习这一重要主题的良好参考。

## 常用元字符示例

`[0-9]` — 说明：匹配所有数字 0–9 的单个实例。

示例：查找字母 c 和字母 t 的所有实例，并在它们之间包含任意 0 到 9 之间的单个数字。

```
c[0-9]t
```

测试文件的结果：

```
dc9gt4
```

`[d-m7-9]` — 说明：匹配字符 d 到 m 或 7 到 9 之间的任意单个字符。这说明了这些命令是如何进行分组的。

示例：查找字母 c 和字母 t 的所有实例，并在它们之间包含 c 到 t 之间的任意单个字母或 0 到 4 之间的任意单个数字。

```
c[c-t0-4]t
```

测试文件的结果：

| Simplicity | dc9gt4 |
|---|---|
| apricot | cccot |
| cot | ccccot |
| simplicity | |

这里列出的元字符通常是常用的，并且在大多数命令中都可用。并不是所有的元字符或正则表达式都能在每个程序中使用，有时程序内部只支持元字符的子集。请阅读你将要使用的命令的 man 页，以确定其对元字符的支持。

元字符和正则表达式通常用于以下命令（尽管还有其他命令）：

```
awk      fgrep
ed       less
emacs    more
expr     sed
grep     vi
egrep
```

### 使用 SFTP 和 FTP

SFTP（安全文件传输协议）和 FTP（文件传输协议）是 Unix 系统之间传输文件的两种主要协议。`sftp` 和 `ftp` 命令的语法与 `telnet` 和 `ssh` 类似，即你启动命令并识别想要登录的位置。例如，要连接到名为 darwin 的 Mac OS X 机器（IP 地址为 192.168.1.58 的远程机器），你需要：

```
sftp 192.168.1.58
```

或者

```
sftp darwin
```

输出将如图 8-1 所示。

```
Session Edit View Bookmarks Settings Help
[beginningunix@linux beginningunix~]$ sftp 192.168.1.58
Connecting to 192.168.1.58...
beginningunix@192.168.1.58's password:
sftp> _
```

图 8-1

对于 `ftp`，你输入：

```
ftp 192.168.1.58
```

或者

```
ftp darwin
```

如果你输入后者，输出将类似于：

```
$ ftp darwin
connected to darwin
Name (darwin:beginningunix): beginningunix
331 Password required for beginningunix
Password:
230-
  Welcome to Darwin!
  230 User beginningunix logged in.
Remote system type is Unix
Using binary mode to transfer files.
ftp> _
```

图 8-2 显示了 `ftp 192.168.1.58` 命令的输出。你可以看到它几乎完全相同，区别在于使用了机器的 IP 地址而不是名称（darwin）。

对于 `ftp darwin` 示例，以下是从初始命令开始所发生的事件序列：

```
$ ftp darwin

beginningunix@linux beginningunix$
[beginningunix@linux beginningunix$
[beginningunix@linux beginningunix]$ ftp 192.168.1.58
Connected to 192.168.1.58
220 to 192.168.1.58 FTP server (tnftpd 20040810) ready.
502 RFC 2228 authentication not implemented.
502 RFC 2228 authentication not implemented.
KERBEROS_V4 rejected as an authentication type
Name (darwin:beginningunix): beginningunix
331 Password required for beginningunix
331 Password required for beginningunix:
Password:
230-
  Welcome to Darwin!
  230 User beginningunix logged in.
Remote system type is Unix
Using binary mode to transfer files.
ftp> _
```

## 文件传输操作

要从远程 FTP 或 SFTP 服务器检索文件，请使用 `get` 命令。以下是从远程 ftp 服务器 (darwin) 获取文件 `/home/myfiles/myfile.txt` 的示例：

```
ftp> get myfile.txt
200 PORT command successful
150 Opening Binary mode data connection for 'myfile.txt' (722 bytes).
226 Transfer complete.
722 bytes received in 0.036 seconds (19 Kbytes/s)
221 Thank you for using the FTP service on Darwin
ftp>
```

第一行包含 `get` 命令以及要检索的远程文件名 (myfile.txt)，该文件将被检索并放置在本地系统的当前目录中。远程系统报告命令执行成功（200 PORT command successful）。第三行显示下载开始，且文件大小为 722 字节。系统报告传输完成，然后告诉你详细信息：如何下载文件以及速度是多少。第六行是一句简单的问候语，感谢你使用该系统。

如果你在输入 `get` 命令之前输入 `hash` 命令，你将看到一系列连续的哈希标记 (`#`)，指示下载进度，对于大文件，这可以帮助判断 FTP 会话没有挂死。

你将返回到命令提示符 (`ftp>`)，可以执行其他 FTP 命令。在本示例中，`quit` 命令将终止 FTP 会话，结束你与远程机器的连接并将你返回本地系统，如提示符所示：

```
ftp> quit
$
```

`sftp` 命令的操作方式与 `ftp` 几乎相同，并提供类似的输出，但它还提供了设置安全、无密码登录和其他功能。FTP 和 SFTP 的主要区别在于 FTP 的所有操作都是未加密或以明文进行的，而 SFTP 使用加密，隐藏机器之间传输的信息和数据。你只需要使用 `sftp` 代替 `ftp` 来建立连接。你的会话将显示 `sftp` 提示符而不是 `ftp`。SFTP 相比 FTP 有许多优势；你可以在 www.openssh.org 了解更多信息。

# 高级命令

你会发现自己经常使用本节中介绍的命令，因为它们为你的 Unix 工作增加了大量功能。

## Grep

`grep` 是 Unix 中最实用的命令之一。它在文件中搜索你指定的序列然后打印结果。这看起来可能微不足道，但你可能会发现自己每天都在使用这个命令对文件进行搜索。

`grep` 是 "global expression print"（全局表达式打印）的缩写，源于 `ed` (pre-vi) 编辑器的命令集，由 `g/re/p` 命令启动。该命令序列由于使用过于频繁，因此人们决定创建一个具有搜索和打印功能的独立命令。整合后的命令就是 `grep`。

`grep` 的命令结构为：

```
grep string_to_search_for file_search
```

一个简单的 `grep` 命令是在 `/etc` 目录及其子目录中搜索 `root` 单词：

```
grep root /etc/*
```

这将导致大量的输出，因为正如你所猜的，有很多文件包含 `root` 单词。`grep` 支持使用之前描述的大多数元字符，具体取决于你使用的命令版本。

`grep` 还有一个 `-v` 参数，允许你搜索除指定字符串以外的所有内容。要搜索 `/etc/passwd` 中除 `root` 字符串以外的所有账户，你需要输入：

```
grep -v root /etc/passwd
```

输出将显示 `/etc/passwd` 文件中不包含 `root` 字符串的内容。

`grep` 还可以与其他命令结合，如下例所示：

```
cat /etc/passwd | grep root
```

这产生的输出与前一个命令不带 `-v` 选项的结果相同，但演示了你如何使用 `grep` 从另一个命令的输出中搜索特定字符。`grep` 命令可以与其他几乎任何命令结合以创建有用的输出。

## find

`find` 命令用于在目录结构中查找文件。`find` 的语法为：

```
find path_to_look_in options
```

要在 `/etc` 目录中查找 `passwd` 文件，可以使用 `-name` 参数：

```
find /etc -name passwd
```

结果输出将匹配指定路径目录及其子目录中找到的任何项。

`find` 命令带有许多选项。下表描述了最常用的几个：

| 选项 | 描述 |
|---|---|
| `--help` | 显示 `find` 命令的帮助信息。 |
| `--maxdepth n` | 目录结构深度为 n 层。例如，如果只想搜索列出的目录而不搜索子目录，则使用 `--maxdepth 0`。 |
| `--mindepth n` | 至少进入 n 层子目录 |
| `--mount` | 防止跨其他文件系统搜索（例如远程挂载的系统）。搜索多个不同的文件系统网络资源。 |

搜索文件时还有其他选项；请参阅帮助页 (man pages) 获取更多信息。下表列出了 `find` 命令可用的一些测试（精炼输出的参数）。这些测试可以与 `find` 命令配合使用。

| 测试 | 描述 |
|---|---|
| `+n` | 搜索大于数字 n 的任何内容。 |
| `-n` | 搜索小于数字 n 的任何内容。 |
| `n` | 搜索精确匹配数字 n 的任何内容。 |
| `-amin n` | 搜索 n 分钟前最后访问的文件。 |
| `-atime n` | 搜索 n 天前最后访问的文件。 |
| `-fstype` | 搜索文件系统类型。 |
| `-gid n` | 搜索组 ID (gid) 等于 n 的文件。 |
| `-group_name` | 搜索组名。 |
| `-name` | 搜索文件名。 |
| `-perm` | 搜索权限模式。 |
| `-size n` | 搜索大小为 n 的文件。 |
| `-type` | 搜索类型。选项包括块设备 b、字符设备、目录 d、命名管道 p、文件 f、符号链接 l 和套接 s。 |
| `-uid n` | 搜索用户 ID (uid) 等于 n 的文件。 |
| `-user` | 搜索用户名。 |

还有许多其他选项，包括一些用于特殊格式输出的以及一些使用正则表达式的。例如，要在 `/home` 目录中查找所有属于用户 `beginningunix` 的文件可以使用类似的命令：

```
find /home -user beginningunix
```

假设你的系统管理员联系你清理主目录空间，你不确定哪些文件可能是问题所在。要搜索大于 2,000,000 千字节（约 2GB）的文件，你可以使用以下命令查找符合条件的文件：

```
find /home -size +2000000k
```
