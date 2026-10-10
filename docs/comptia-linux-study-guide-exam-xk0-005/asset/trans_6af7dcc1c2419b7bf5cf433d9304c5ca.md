
发送 82.12K 字节，接收 54 字节，164.35K 字节/秒
总大小为 81.92K，加速比为 1.00

$ **ls TarStorage**

Project4x.tar	ProjectVerify.tar

$

`rsync` 工具真正的优势在于在网络备份过程中保护文件。

为了实现安全的远程复制，你需要在远程系统上启动并运行 OpenSSH 服务。此外，必须在本地和远程机器上都安装 `rsync` 工具。使用 `rsync` 命令通过网络安全复制文件的示例参见清单 12.16。

# **清单 12.16** 使用 `rsync` 远程备份文件

```
$ ls -sh *.tar

40K Project4x.tar	40K ProjectVerify.tar

$

$ rsync -avP -e ssh *.tar user1@192.168.0.104:

user1@192.168.0.104's password:

sending incremental file list

Project4x.tar

	40,960 100%	7.81MB/s	0:00:00 (xfr#1, to-chk=1/2)

ProjectVerify.tar

	40,960 100%	39.06MB/s	0:00:00 (xfr#2, to-chk=0/2)

sent 82,121 bytes	received 54 bytes	18,261.11 bytes/sec

total size is 81,920	speedup is 1.00

$
```

注意清单 12.16 中 `rsync` 工具使用了 `-avP` 选项。这些选项不仅将复制模式设置为归档模式，还会在文件传输过程中提供详细信息。此清单中需要注意的重要开关是 `-e` 选项。该选项确定使用 OpenSSH 进行传输，并有效地创建了一个加密隧道，使得任何嗅探网络的人都无法看到流经的数据。命令中的 `*.tar` 仅选择要复制到远程机器的本地文件。`rsync` 命令中的最后一个参数指定了以下内容：

- 用于传输的远程系统上的用户帐户（`user1`）。
- 远程系统的 IPv4 地址，但也可以使用主机名。
- 文件的放置位置。在这种情况下，是主目录，由 `~` 符号表示。

还请注意最后一个参数中，IPv4 地址和目录符号之间有一个必需的冒号（`:`）。如果你没有包含这个冒号，你将把文件复制到一个名为 `user1@192.168.0.104~` 的新文件中，位于本地目录中。

![](img/c0a399aca0d18f8822d714ad0a173123_447_0.png)

> `rsync` 工具默认使用 OpenSSH。然而，使用 `-e` 选项是个好习惯。如果你使用任何 `ssh` 命令选项时尤其如此，例如指定要使用的 OpenSSH 密钥或使用不同于默认端口 22 的端口。第 16 章“查看访问和身份验证方法”中将更详细地介绍 OpenSSH。

`rsync` 工具对于将大文件复制到远程介质也非常有用。如果你有快速的 CPU 但网络连接缓慢，可以使用 `rsync -z` 选项压缩传输的数据，从而进一步加快速度。这并不是使用 `gzip` 压缩，而是通过 `zlib` 压缩库应用压缩。你可以在 `https://zlib.net` 找到更多关于 `zlib` 的信息。

## 保护场外/系统外备份

在商业中，数据就是金钱。因此，不仅创建数据归档至关重要，保护它们也至关重要。当备份传输到远程位置时，还有几种额外的方法来保护你的备份。

除了 `rsync`，你还可以使用基于安全复制协议 (SCP) 的 `scp` 工具。此外，基于 SSH 文件传输协议 (SFTP) 的 `sftp` 程序也是安全传输归档文件的一种手段。我们将在以下章节中介绍这两个工具。

### 通过 `scp` 安全复制

`scp` 工具专为以非交互方式在网络上两个系统之间快速传输文件而设计。该程序使用 OpenSSH。

它最适合用于需要即时安全复制的小文件，因为如果操作中途中断，它无法从中断处恢复。对于较大的文件或数量更多的文件，最好使用 `rsync` 或 `sftp` 工具。

有一些相当有用的 `scp` 选项。表 12.6 列出了一些常用开关。

### 表 12.6 *scp* 命令常用复制选项

| 短选项 | 描述 |
| :---- | :---- |
| -C | 在传输期间压缩文件数据 |
| -p | 保留文件的访问和修改时间以及文件权限 |
| -r | 复制目录的内容，并且对于原始目录树中的任何子目录，连续复制其内容（递归） |
| -v | 显示有关命令执行的详细信息 |

从本地系统将文件安全复制到远程系统相当简单。你需要在远程系统上启动并运行 OpenSSH 服务。示例参见清单 12.17。

# 清单 12.17 使用 *scp* 将文件安全复制到远程系统

```
$ scp Project42.txt user1@192.168.0.104:~
user1@192.168.0.104's password:
Project42.txt 100% 29kB 20.5MB/s 00:00
$
```

请注意，为了完成此任务，没有使用任何 *scp* 命令选项。-v 选项提供了很多在这种情况下不需要的信息。

> 警告 *scp* 工具将覆盖与正在传输的文件同名的任何远程文件，而不会询问，甚至不会显示消息说明这一事实。在使用 *scp* 复制文件时，你需要注意不要覆盖任何现有文件。

使用 *scp* 的一个便捷方法是将从一台远程机器复制文件到另一台远程机器。示例参见清单 12.18。

# 清单 12.18 使用 *scp* 在远程系统之间安全复制文件

```
$ ip addr show | grep 192 | cut -d" " -f6
192.168.0.101/24
$

$ scp user1@192.168.0.104:Project42.txt user1@192.168.0.103:~
user1@192.168.0.104's password:
user1@192.168.0.103's password:
Project42.txt           100%  29KB  4.8MB/s   00:00
Connection to 192.168.0.104 closed.
$
```

首先，在清单 12.18 中，使用 `ip addr` show 命令检查当前机器的 IPv4 地址。然后使用 `scp` 工具将 `Project42.txt` 文件从一台远程机器复制到另一台。当然，你必须在这台机器上运行 OpenSSH，并且有一个可以登录的用户帐户。

## 通过 sftp 安全传输

` sftp` 工具也允许你在网络上安全传输文件。然而，它是为更交互式的体验而设计的。使用 `sftp`，你可以按需创建目录，立即检查传输的文件，确定远程系统的当前工作目录等等。此外，此程序使用 OpenSSH。

为了了解这种交互式工具的工作方式，最好看一下一个简单的示例。示例参见清单 12.19。

# **清单 12.19** 使用 sftp 访问远程系统

```
$ sftp Christine@192.168.0.104
Christine@192.168.0.104's password:
Connected to 192.168.0.104.
sftp> 
sftp> bye
$
```

在清单 12.19 中，`sftp` 工具与用户名和远程主机的 IPv4 地址一起使用。一旦输入了用户帐户的正确密码，就会显示 `sftp` 工具的提示符。此时，你已连接到远程系统。在提示符下，你可以输入任何命令，包括 `help` 来查看所有可能命令的显示，以及如清单所示的 `bye` 退出工具。一旦你退出了工具，你就不再连接到远程系统。

在使用 `sftp` 交互式工具之前，了解一些更常见的命令是很有帮助的。表 12.7 列出了一些。

# **表 12.7** sftp 命令常用命令

| 命令 | 描述 |
| :------ | :---------- |
| bye | 退出远程系统并退出工具。 |
| exit | 退出远程系统并退出工具。 |
| get | 从远程系统获取文件（或文件组）并将其（它们）存储在本地上。称为下载。 |
| reget | 恢复中断的 get 操作。 |
| put | 从本地系统发送文件（或文件组）并将其（它们）存储在远程系统上。称为*上传*。 |
| reput | 恢复中断的 put 操作。 |
| ls | 显示远程系统当前工作目录中的文件。 |
| lls | 显示本地系统当前工作目录中的文件。 |
| mkdir | 在远程系统上创建目录。 |
| lmkdir | 在本地系统上创建目录。 |
| progress | 切换进度显示的开/关。（默认为开。） |

如果你过去从未使用过 FTP 交互程序，那么前几次使用 sftp 工具时可能会有一点棘手。将一个本地文件发送到远程系统的示例参见清单 12.20。

# **清单 12.20** 使用 sftp 将文件复制到远程系统

```
$ sftp Christine@192.168.0.104
Christine@192.168.0.104's password:
Connected to 192.168.0.104.
sftp> ls
Desktop Documents Downloads Music Pictures Public Templates Videos
sftp> lls
AccountAudit.txt Grades.txt Project43.txt ProjectVerify.tar
err.txt Life Project44.txt TarStorage
Everything NoLoginAccts.txt Project45.txt Universe
Extract Project42_Inc.txt Project46.txt
FullArchive.snar Project42.txt Project4x.tar
Galaxy Project42.tzx Projects
sftp> 
sftp> put Project4x.tar
Uploading Project4x.tar to /home/Christine/Project4x.tar
Project4x.tar 100% 40kB 15.8MB/s 00:00
sftp>
```
