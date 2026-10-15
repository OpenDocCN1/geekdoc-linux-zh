
$ cd ..

$pwd

/home

# mkdir 命令

要创建一个新目录，你使用 `mkdir` 命令。它的语法如下：

```
mkdir directory
```

这里是一个示例，它会在当前目录下创建一个名为 `images` 的子目录：

```
$ mkdir images
```

这个示例创建了一个名为 `/home/doug/images` 的目录：

```
$ mkdir /home/doug/images
```

# rmdir 命令

`rmdir` 命令删除目录。它的语法如下：

```
rmdir directory
```

## 734 目录与文件处理命令

这里有一个示例：

```
$ rmdir /home/doug/images
```

在这里，`/home/doug/images` 目录被删除了。注意，该目录必须为空才能删除，所以你必须先删除该目录中的任何文件。

# ls 命令

`ls` 命令列出当前目录的内容。语法如下：

```
ls [options] directory
```

以下段落描述了 `ls` 命令更重要的选项：

- `-a`: 列出目录中的所有文件，包括以点开头的文件。
- `-c`: 按文件最后修改时间排序条目。
- `-d`: 仅列出目录名。
- `-1`: 以长格式显示文件。
- `-r`: 反序显示文件。
- `-R`: 列出所有子目录、子目录的子目录以及子目录的子目录的子目录……换句话说，递归列出子目录。
- `-s`: 按文件大小排序。
- `-S`: 按大小排序文件。
- `-t`: 按最后修改时间排序文件。
- `-u`: 按最后访问时间排序文件。
- `-X`: 按文件扩展名排序文件。

在不带参数的情况下，`ls` 命令列出当前目录下的所有文件，如下：

```
$ pwd

/etc/mail

$ ls

access helpfile Makefile submit.cf virtertable

access.db local-hosts sendmail.bak virtertable.db

domaintable mailertable sendmail.mc sendmail.mc

domaintable.db mailertable.db statistics trusted-users
```

## 目录与文件处理命令 735

你可以通过输入文件名（可以包含通配符）来限制显示为某些特定文件。例如：

```
$ ls a*
access      access.db
```

你也可以像这样指定你想要显示的目录：

```
$ ls /etc/httpd
conf.d  logs  run
```

要显示目录中文件的详细信息，在例例中使用了 `-1` 选项：

```
$ ls /etc/mail/s -1
-rw-r-r--  root  root  57427 Jul 19 16:35 sendmail.cf
-rw-r-r--  root  root   5798 Feb 24 16:35 sendmail.mc
-rw-r-r--  root  root    628 Jul 24 17:21 statistics
-rw-r-r--  root  root  39028 Jul 19 17:28 submit.cf
-r--r--r--  root  root  39077 Feb 24 16:15 submit.cf.bak
-rw-r-r--  root  root    953 Feb 24 16:15 submit.mc
```

# cp 命令

`cp` 命令复制文件。语法如下：

```
cp [options] source-file destination-file
```

以下列表描述了 `ls` 命令（注：此处原文可能有误，应为cp）更重要的选项：

- `-a`: 等同于 `-dpR`。

## 736 目录与文件处理命令

要在同一目录内复制文件，可以这样使用 `cp`：

```
$ cp sendmail.cf sendmail.cf.backup
```

如果你想在不更改文件名的情况下将文件复制到另一个目录，这样使用 `cp`：

```
$ cp sendmail.cf /home/doug
```

你可以使用通配符复制多个文件：

```
$ cp send* /home/doug
```

要包含源文件子目录中的文件，请使用 `-R` 选项，如下：

```
$ cp -R /etc/*.cf /home/doug
```

在这个示例中，`/etc` 目录或其任何子目录下所有以 `.cf` 结尾的文件都被复制到了 `/home/doug`。

# rm 命令

`rm` 命令删除文件。语法如下：

```
rm file
```

以下段落描述了这些选项：

- `-f`: 强制删除且不提示。
- `-i`: 在删除前进行交互式询问。
- `-r`: 递归删除目录。

删除文件，使用：

```
$ rm filename
```

删除多个文件，使用：

```
$ rm file1 file2 file3
```

删除空目录，使用：

```
$ rmdir directory
```

删除目录及其所有内容，使用：

```
$ rm -r directory
```

# 740 用于软件包和服务的命令

列出所有服务需要一些时间，但在命令执行完成后，你可以滚动列表以找到你正在寻找的服务。

表 8-3 列出了一些常用的服务。

| 服务 | 描述 |
| --- | --- |
| atd | 运行由 命令调度的任务。 |
| autof | 自动挂载文件系统。 |
| crond | 在指定时间运行程序。 |
| dhcpd | DHCP 服务器。 |
| finger | Internet finger 服务。 |
| httpd | Apache Web 服务器。 |
| imap | IMAP 邮件协议。 |
| imaps | 安全的 IMAP 服务 (SSL)。 |
| ipop3 | POP3 邮件协议。 |
| iptables | 防火墙的自动包过滤。 |
| isdn | SDN 服务。 |
| named | Bind DNS 服务器。 |
| netfs | 网络文件系统。 |
| network | 激活和禁用所有网络接口。 |
| nfs | 原生 UNIX/网络文件共享。 |
| pop3s | 安全的 POP3 服务 (SSL)。 |
| sendmail | Sendmail 服务。 |
| smb | Samba 文件和打印机共享服务。 |
| snmp | 简单网络管理协议。 |
| telnet | Telnet 服务器。 |

# rpm 命令

Rpm 是红帽软件包管理器（Red Hat Package Manager），这是一个简化 Linux 系统上软件包管理任务的工具。虽然 rpm 最初是为 Red Hat Linux 开发的，但现在出现在许多 Linux 发行版中，包括 Fedora（它当然是基于 Red Hat 发行版的）。

以下是查询软件包状态的基本语法：

```
rpm -q [options] package
```

## 741 用户管理命令

要安装、升级或删除软件包，基本语法类似于所示：
`rpm [ -i | -u | -e ] [options] package-file`

你可以在 rpm 命令中使用一些选项，但最常用的是：

- `-v`: 显示冗余输出。你完全可以顺便在 rpm 运行时了解它正在做什么。
- `-h`: 定期显示哈希值 (#) 以让你确认程序没有崩溃。

你可以使用 `-q` 切换来通过 rpm 确定系统上已安装软件包的状态。例如，要查找安装的 Sendmail 版本，请使用此命令：

```
$ rpm -q send*
Sendmail-8.12.8-4
```

注意，你可以在包名中使用通配符。如果你没有找到与你提供的包名匹配的软件包，将收到 `package not installed`（软件包未安装）的消息。

要安装软件包，使用 `-i` 切换和指示软件包文件位置的通配符文件名。使用 `v` 和 `h` 切换也是好主意。例如，从挂载的 CD-ROM 驱动器安装 Sendmail，使用此命令：

```
$ rpm -ivh /mnt/cdrom/RedHat/RPMS/sendmail*
```

如果你想更新软件包到新版本，可以使用 `-u` 切换代替 `-i` 切换：

```
$ rpm -uvh /mnt/cdrom/RedHat/RPMS/sendmail*
```

最后，你可以使用 `-e` 切换删除软件包：

```
$ rpm -e send*
```
