

# 第15章 ✦ Linux 网络 431

当我们把 SSH 公钥复制到 `authorized_keys` 文件后，我们可以使用密钥短语而不是密码登录远程服务器，如下所示：

```
justin@bible:-> ssh 192.168.131.70
Enter passphrase for key '/home/justin/.ssh/id_rsa':
Last login: Tue Jul 6 04:31 from bible.com
```
注意，这里被要求输入短语而不是密码。SSH 服务器不会查询数据库，但因为我们有有效的密钥对，它接受了请求。如果我们没有输入密钥对，就可以可以在任何用户干预的情况下访问系统。尽管不像传统的系统那样安全，当你需要编写一个不需要用户干预自动登录到远程服务器的脚本时，它是无价之宝。

# 安全拷贝 (Secure Copy)

安全拷贝是 SSH 系统的扩展扩展，它使用你的公钥（如果可用）从和到远程服务器复制文件。我们已经遇到过 `scp` 命令，它与 SSH 非常相似之处在于它定义了你连接的位置（使用 `username@server` 符号）。

该命令的特殊之处在于：

```
scp myfile justin@palmcoder.net:/etc/
```

此命令将 `myfile` 复制到服务器 `palmcoder.net` 的 `/etc/` 目录。如果你指定的是目录，就会提示你输入短语。SCP 能够复制整个目录，正如 `scp` 命令所示。如果要复制目录，你需要在命令行中添加 `-r` 以进行递归拷贝：

```
scp -r mydirectory justin@palmcoder.net:/tmp/
```

此命令将 `mydirectory` 的所有内容复制到 `palmcoder.net` 的 `/tmp` 目录。使用的冒号（`:`）非常重要，如果在指定的目录末尾没有正斜杠（`/`），我们只会复制目录的内容，而不是目录本身。请注意这一点，因为如果漏掉了正斜杠，很容易复制预期之外的所有内容。

如果你想确保同步时从源服务器删除的任何文件在本地机器上也确实被删除，你需要在命令行选项中添加 `-delete` 参数。

# rsync

两个服务器可能定期同步某些数据是非常常见的。你有几种方法可以做到，包括文件传输协议 (FTP)、网络文件系统 (NFS) 或 `scp`。这些协议的问题是，很难知道上次同步以来文件是否发生了变化，即使它们没有变化仍需复制文件。

rsync 是一种为了解决这些问题而设计的有效传输协议。我们多次使用它从一个服务器备份到另一台物理机器，当处理全天可能变化的数 GB 数据时，它是非常有用的。

rsync 的另一个强大功能是你可以压缩从服务器发送的数据流。这有助于减少同步数据的时间。例如，rsync 非常擅长将网站同步到我们笔记本电脑上的本地副本。参见列表 15-13。

# 列表 15-13：同步网站目录

```
bible:/www # rsync -avrz -e ssh www.palmcoder.net:/var/www/palmcoder/blogimages /
receiving file list ... done
blogimages/
blogimages/DSCN0156.thumb.jpg
blogimages/DSCN0191.thumb.jpg
blogimages/DSCN0718.jpg
blogimages/dscn0456.jpg
blogimages/palmcoder.gif

wrote 96 bytes read 92643 bytes 10910.47 bytes/sec
total size is 96350 speedup is 1.04
```

你可以看到我们选择复制一个包含多个文件的单个目录。在这个示例中，`rsync` 命令使用的参数 `-azrv` 分别对应：

- -a：启用归档模式，保留你正在复制的文件的所有属性。
- -v：详细模式，以便你可以看到正在复制的文件。
- -r：递归拷贝，遍历你正在复制的目录的结构。
- -z：压缩数据流。

在这个示例中，我们还告诉 rsync 使用 ssh 连接到服务器。虽然我们可以使用 rsync 服务器，但大多数人只使用 ssh 传输数据，因为许多服务器运行的是 ssh 而不是 rsync 服务器。

在示例指定服务器 (`www.palmcoder.net`) 时，我们特别指定了要复制的目录，并用冒号（`:`）隔开。由于我们没有在博客目录末尾加上正斜杠（`/`），rsync 将该目录及其内容复制到我们的本地机器。如果指定的目录后面加上了正斜杠，我们只会复制目录的内容而不是目录本身。要警惕这一点，因为如果漏掉正斜杠，很容易复制预期之外的所有内容。

# wget

如果你需要快速从 FTP 下载网页或文件，可以使用 `wget`。如果你在没有网络浏览器（这很常见）的情况下需要将文件获取到服务器，它是一个非常棒的工具。

`wget` 命令仅用于通过 HTTP 和 FTP 传输文件。不要将其与像 `rsync` 这样的通用网络拷贝系统混淆。

在最简单的形式，你只需要将想要下载的 URL 传递给 `wget` 命令（参见列表 15-14）。这将指定的 URL 下载到本地目录。

# 通过 HTTP 下载文件到你的本地服务器

```
bible:- # www.palmcoder.net/index.php
--03:26 - http://www.palmcoder.net/index.php
"index.php"
Resolving www.palmcoder.net...212.13.208.115
Connecting to www.palmcoder.net...212.13.208.115
... (此处省略重复的连接日志) ...
```

