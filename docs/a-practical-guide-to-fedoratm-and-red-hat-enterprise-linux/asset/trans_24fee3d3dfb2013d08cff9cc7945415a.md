

## ssh：登录远程系统或在其上执行命令

ssh 命令行的格式如下：

```
ssh [options] [user@]host [command]
```

其中，host 是你想要连接的 OpenSSH 服务器（即远程系统）的名称，它是唯一必需的参数。host 可以是本地系统名称、互联网上某系统的全限定域名（FQDN，见第 1250 页）或 IP 地址。

使用命令 `ssh host`，你可以使用与本地系统相同的用户名登录到远程系统 host。远程系统会显示 shell 提示符，你可以在 host 上运行命令。输入命令 `exit` 以关闭与 host 的连接并返回到本地系统的提示符。当你希望使用与本地系统不同的用户名登录时，请包含 `user@`。根据服务器的配置情况，你可能需要提供在远程系统上使用的密码。

当包含 `command` 时，`ssh` 会登录到 host，执行 `command`，关闭与 host 的连接，并将控制权返回给本地系统。远程系统永远不会显示 shell 提示符。

在下面的示例中，登录在 guava 上的 Sam 使用 `ssh` 登录到 plum，输入显示系统名称和类型的 `uname` 命令，并使用 `exit` 关闭与 plum 的连接并返回到本地系统的提示符：

```
[sam@guava ~]$ ssh plum
sam@plum's password:
Last login: Wed Jun 12 16:55:47 2013 from guava
[sam@plum ~]$ uname -nm
plum x86_64
[sam@plum ~]$ exit
logout
Connection to plum closed.
[sam@guava ~]$  
```

以下示例使用 `ls` 显示远程系统 plum 上 memos 目录中的文件列表。该示例假设运行命令的用户（Sam）在 plum 上有登录权限，且 memos 目录位于 Sam 在 plum 上的主目录中：

```
$ ssh plum ls memos
sam@plum's password:
memo_0921
memo_draft
$ 
```

当你运行 `ssh` 时，在远程系统上运行的命令的标准输出会被传递给本地 shell，就像该命令在本地系统上运行一样。与所有 shell 命令一样，你必须对不希望本地 shell 解释的特殊字符进行引号转义。

在下一个示例中，在远程系统上运行的 `ls` 命令的标准输出被发送到本地系统的 `ls.out` 文件。

```
$ ssh plum ls memos > ls.out
sam@plum's password:
$ cat ls.out
memo_0921
memo_draft
```

在前面的 `ssh` 命令中，重定向符号（`>`）没有加引号，因此它由本地 shell 解释，并在本地系统上创建 `ls.out` 文件。下一条命令类似，但重定向符号加了引号，因此本地 shell 不会解释它，而是将其传递给远程 shell。第一条命令在远程系统上创建 `ls.out2` 文件，第二条命令显示该文件。

```
$ ssh plum 'ls memos > ls.out2'
sam@plum's password:
$ ssh plum cat ls.out2
sam@plum's password:
memo_0921
memo_draft
```

对于下一个示例，假设本地系统的工作目录中有一个名为 `memo.new` 的文件。你不记得这个文件是否包含某些更改，或者你是否在 plum 上的 memos 目录中的文件 `memo.draft` 上做了这些更改。你可以将 `memo.draft` 复制到本地系统，并对两个文件运行 `diff`（见第 227 页），但这样你会在两个系统之间分散三个类似的文件副本。如果在完成后不仔细删除旧副本，你几天后可能又会感到困惑。你可以使用 `ssh` 代替复制文件。这个示例表明两个文件之间只有日期行不同：

```
$ ssh plum cat memos/memo.draft | diff memo.new -
sam@plum's password:
1c1
< Wed Jun 14 12:22:14 PDT 2013
---
> Wed Jun 12 17:05:51 PDT 2013
```

在前面的示例中，plum 上 `cat` 命令的输出通过本地系统上的管道发送到在本地系统上运行的 `diff`，它将本地文件 `memo.new` 与标准输入（`-`）进行比较。以下命令行具有相同的效果，但会导致 `diff` 在远程系统上运行：

```
$ cat memo.new | ssh plum diff - memos/memo.draft
sam@plum's password:
1c1
< Wed Jun 14 12:22:14 PDT 2013
---
> Wed Jun 12 17:05:51 PDT 2013
```

远程系统上 `diff` 的标准输出被发送到本地 shell，并在屏幕上显示出来（因为它没有被重定向）。

## 选项

本节描述了你可以与 `ssh` 一起使用的一些选项。

- `-C`（压缩）：启用压缩（见第 710 页）。在 ssh 的商业版本中，`-C` 禁用压缩，而 `+C` 启用压缩。
- `-f`（非前台）：在询问密码后、执行命令前将 ssh 发送到后台。当你希望在后台运行命令但必须提供密码时很有用。隐含 `-n`。
- `-i filename`（标识）：指示 ssh 从 `filename` 读取私钥，而不是从 `~/.ssh/id_dsa` 或 `~/.ssh/id_rsa` 读取用于自动登录（密钥，见第 700 页）。参见第 680 页的示例。
- `-L`：将本地系统上的端口转发到远程系统。更多信息请参见第 707 页的“隧道/端口转发”。
- `-l user`（登录）：尝试以 `user` 身份登录。
- `-n`（空）：将 ssh 的标准输入重定向为来自 `/dev/null`。在后台运行 ssh（`-f` 选项）时必需。
- `-o option`（选项）：以配置文件（见第 698 页）中使用的格式指定 `option`。
- `-p port`（端口）：指定连接所在的远程主机端口。使用配置文件中的 host 声明（见第 699 页），你可以为每个连接的系统指定不同的端口。
- `-R`：将远程系统上的端口转发到本地客户端。更多信息请参见第 707 页的“隧道/端口转发”。
- `-t`（tty）：为远程系统上的 ssh 进程分配一个伪 tty（终端）。如果没有此选项，当你在远程系统上运行命令时，ssh 不会为该进程分配 tty（终端）。相反，它将远程进程的标准输入和标准输出附加到 ssh 会话——这通常是你想要的，但并非总是如此。此选项强制 ssh 在远程系统上分配一个 tty，以便需要 tty 的程序能够正常工作。
- `-v`（详细）：显示关于连接和传输的调试消息。当事情不按预期进行时很有用。重复此选项最多三次以增加详细程度。
- `-X`（X11）：启用不可信 X11 转发。如果在配置文件中启用了不可信 X11 转发，则不需要此选项。更多信息请参见第 707 页的“转发 X11”。
- `-x`（X11）：关闭 X11 转发。
- `-Y`（X11trusted）：启用可信 X11 转发。如果在配置文件中启用了可信 X11 转发，则不需要此选项。更多信息请参见第 707 页的“转发 X11”。

## scp：将文件复制到远程系统及其副本

`scp`（安全复制）实用程序通过网络将一个普通文件或目录从一个系统复制到另一个系统；两个系统都可以是远程的。此实用程序使用 `ssh` 传输文件，并采用与 `ssh` 相同的认证机制；因此，它提供与 `ssh` 相同的安全性。当需要密码时，`scp` 实用程序会要求输入密码。`scp` 命令的格式为

```
scp [user@]from-host:source-file [user@]to-host:destination-file
```

其中 `from-host` 是你复制文件来源系统的名称，`to-host` 是你复制文件目标系统的名称。`from-host` 和 `to-host` 参数可以是本地系统名称、互联网上系统的全限定域名（FQDN，见第 1250 页）或 IP 地址。当你未指定 host 时，`scp` 假设是本地系统。任一系统上的 `user` 默认为发出命令的本地系统用户；你可以使用 `user@` 指定不同的用户。

`source-file` 是你正在复制的文件，而 `destination-file` 是生成的副本。请确保你对正在复制的文件具有读取权限，对正在复制到的目录具有写入权限。你可以将普通文件或目录指定为相对路径或绝对路径。（相对路径是相对于指定目录或隐式用户的主目录而言的。）当 `source-file` 是目录时，你必须使用 `-r` 选项来复制其内容。当 `destination-file` 是目录时，每个源文件保持其简单文件名。当缺少 `destination-file` 时，`scp` 假设是用户的主目录。

假设 Sam 在 `plum` 上有一个备用用户名 `s1s`。在以下示例中，Sam 使用 `scp` 将 `plum` 上其 `s1s` 账户主目录中的 `memo.txt` 复制到本地系统工作目录中的 `allmemos` 目录。如果 `allmemos` 不是目录名称，`memo.txt` 将被复制到工作目录中名为 `allmemos` 的文件。

```
$ scp s1s@plum:memo.txt allmemos
s1s@plum's password:
  memo.txt        100%  12KB  12.3KB/s  00:00
```

随着传输的进行，传输的百分比和字节数增加，而剩余时间减少。

### rsync 比 scp 功能强大得多

![](img/243613168ac865b539f12460d966088e_752_0.png)

`rsync` 实用程序比 `scp` 更具可配置性，并默认使用 OpenSSL 安全性。它有许多选项；最常用的选项是 `-a` 和 `-v`。`-a` 选项使 `rsync` 复制普通文件和目录，保留与文件相关的拥有权、组、权限和修改时间。指定 `-a` 选项通常不会造成伤害，而且经常有帮助。`-v` 选项使 `rsync` 在复制文件时列出它们。例如，Sam 可以将前面的命令输入为

```
$ rsync -av s1s@plum:memo.txt allmemos
s1s@plum's password:
  receiving incremental file list
  memo.txt

  sent 30 bytes  received 87495 bytes  19450.00 bytes/sec
  total size is 87395  speedup is 1.00
```

`rsync` 实用程序也比 `scp` 更智能。如果源文件和目标文件存在，`rsync` 仅复制源文件与目标文件不同的部分。当复制更改很少的大文件（例如制作备份时），此功能可以节省大量时间。输出中 `speedup` 后面的数字表示 `rsync` 算法加速文件复制过程的程度。

