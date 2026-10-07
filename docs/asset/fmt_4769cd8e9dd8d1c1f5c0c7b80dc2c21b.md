
```
$ smbclient //phobos/$c -U BOULDER\ben
Password: password
Domain=[BOULDER] OS=[Windows Vista (TM) Business 6001 Pack 1]
Server=[Windows Vista (TM) Business 6.0]
smb:\>
```

一旦您成功登录到文件服务器，就可以使用标准的 ftp 风格命令（如 `get`、`put`、`lcd` 和 `dir`）来导航和传输文件。输入 `?` 查看可用命令完整列表。

# Linux 客户端对 CIFS 的支持

Linux 包含了对 SMB/CIFS 文件系统的直接客户端支持。您可以像挂载任何由内核直接理解的文件系统一样，将 CIFS 共享挂载到您的文件系统树中。例如：

```
$ sudo mount -t cifs -o username=joe /redmont/jos /home/mnt
```

尽管此功能非常有用，但请记住，Windows 概念上将网络工作挂载视为由特定用户建立的（因此是上面的 `username=joe`），而 UNIX 则认为它们更通常属于整个系统。Windows 服务器用户通常无法处理“多个不同的人可能访问挂载的 Windows 共享”这一概念。

从 UNIX 客户端的角度来看，挂载目录中的所有文件都属于挂载它的用户。如果您以 root 身份挂载共享，那么所有文件都属于 root，普通用户可能无法向 Windows 服务器写入内容。

挂载选项 `uid`、`gid`、`fmask` 和 `dmask` 允许您调整这些设置，使所有权和权限位更符合该项共享预期的访问策略。请检查 `mount.cifs` 手页以获取有关此种行为的更多信息。

要允许用户自行挂载 Windows 共享，您可以在 `/etc/fstab` 文件中添加一行如下格式的配置：

```
//redmond/jo /home/joe/mnt cifs
username=joe,fmask=600,dmask=700,noauto 0 0
```

由于此处指定了用户选项，用户现在只需运行以下命令即可挂载文件系统：

```
$ /home/joe/mnt
```

`mount` 会在挂载共享之前提示用户提供密码。

尽管 NFS 是网络文件服务的标准，但在某些情况下，使用 Samba 和 CIFS 在 UNIX 和 Linux 计算机之间共享文件是有意义的。例如，在某些 NFS 版本中允许用户从个人笔记本电脑挂载公司文件系统是危险的。然而，您可以安全地使用 CIFS 让这些笔记本电脑访问其所有者的主目录。

# 30.7 使用 SAMBA 共享打印机

共享简单方法是在 `smb.conf` 中添加一个 `[printers]` 部分；这会让 Samba 共享所有本地打印机。Samba 使用打印命令执行工作，但由于 UNIX并不标准化，您可能需要告诉 Samba 您的服务器使用的是哪种特定的打印系统。要做到这一点，将 `printing` 选项设置为适当的值；检查 `smb.conf` 手页以获取当前支持的打印系统列表。

```
[printers]
; 在将打印文件传递给打印系统之前存储在何处？
path = /var/tmp
```

- NFSv3 安全基于用户在客户端上没有 root 权限且 UID 在客户端和服务器之间匹配的想法。这对于自管理的机器通常不是如此。NFS4 比 NFSv3 有更好的 UID 映射，并且要安全得多。

# 第 30 章

; 所有人可以使用打印机。
guest ok = yes

; 让 Samba 知道此共享是一个打印机。
printable = yes

; 向所有查看的人显示打印机。
browseable = yes

; 告诉 samba 系统在使用什么种类型的打印系统。
printing = cups

有关打印的更多信息，请参见第 26 章。

Windows 客户端现在可以使用这些打印机作为网络打印机，就像它们由 Windows 服务器托管一样。但这里有一个小问题：Windows 将知道它是哪种打印机，并会要求用户选择合适的打印机驱动程序。这导致了许多不知道在这种情况下如何操作的用户产生大量支持请求。如果特定的打印机需要的 Windows 未包含的驱动程序，情况将变得更加耗费支持。

幸运的是，您可以配置 Samba 为 Windows 客户端提供必要的 Windows 打印机驱动程序。要实现此功能，您必须进行一些准备工作以确保 Samba 像打印服务器一样运行，并在 `smb.conf` 文件的 `[global]` 部分添加适当条目：

```
[global]
; 谁是我们的打印机管理员
printer admin = printamd
; 以下默认值是正确的。
disable spoolss = no
; 不要麻烦显示它；你无法添加打印机
show printer wizard = no
; 假设 samba 打印可以
browseable = no
```

# 第 30 章 与 Windows 协作

; 此共享目录下的 DFS 符号链接。
msdfs root = yes
path = /home/dfs/mydfs

您可以在 `/home/dfs/mydfs` 中创建符号链接来设置实际的自动挂载。例如，以下命令将 'jump' 目录创建指向其他服务器上两个目录之一的链接。（注意单引号。它们对于保护反斜杠是必不可少的）。

```
sudo in -s 'mydfs:serverX\shareX,serverY\shareY' jump
```

如果提供了多个源（如此处所示），Windows 将在它们之间进行故障转移。访问 `\servermydfsjump` 的用户现在实际上将从 serverX 上的 shareX 或 serverY 上的 shareY 读取文件，取决于可用性。如果文件系统被导出为可读/可写，您必须确保您有某种机制来同步文件。rsync 在这方面很有帮助。

通过 Samba，您还可以将所有访问特定共享的客户端重定向到不同的服务器。这是 Windows 无法做到的功能。

```
[mydirect]
msdfs root = yes
msdfs proxy = \serverZ\shareZ
```

注意，DFS 仅适用于在所有涉及的服务器上具有相同用户名和密码的用户。

# smbclient：简单的 CIFS 客户端

除了它的许多多服务器功能外，Samba 软件包包含一个名为 `smbclient` 的简单命令行文件传输程序。您可以使用此程序访问任何 Windows 或 Samba 服务器。例如：

```
$ smbclient //phobos/$c -U BOULDER\ben
Password: password
Domain=[BOULDER] OS=[Windows Vista (TM) Business 6001 Pack 1]
Server=[Windows Vista (TM) Business 6.0]
smb:\>
```

一旦您成功登录到文件服务器，就可以使用标准的 ftp 风格命令（如 `get`、`put`、`lcd` 和 `dir`）来导航和传输文件。输入 `?` 查看可用命令完整列表。

# 从命令行安装打印机驱动程序

正如你所猜到的那样，没有 Windows 的情况下，某些步骤是很难重复的，特别是打印机默认值的设置。如果你想在 Samba 服务器上设置几百台打印机，你可能仍然想尝试从命令行进行。命令行配置对于 PostScript 打印机特别有效，因为 Windows PostScript 打印机驱动程序在没有默认配置信息的情况下也能正常。

如果你记录了特定驱动程序所需的文件，就可以从命令行安装该驱动程序。首先，将所需文件复制到 `print$` 共享：

```
$ cd /mydriver
$ smclient -U printadmin '//samba-server/print$' -c "put *"
```

接下来，将驱动程序分配给特定的打印机。假设你有一个带有自定义 PPD 文件的简单 PostScript 打印机：

```
$ rpclient -U printadmin -c ""
addserver \"Windows NT x86\"\Our Custom PS:\nPSCRIPT.DLL:CUSTOM.PPD:PSSUI.DLL:PSCRIPT.HLLP:NULL:SCRIPT.NTF\""
samba-server
```

末尾的反斜杠允许将命令分成多行以保持清晰；如果你愿意，可以省略这些并在一行中输入命令。双引号之前的反斜杠将其与嵌套的引号区分开来。

示例中的长字符串包含了在 Windows 上安装打印机驱动程序时看到的属性框中列出的信息：
字体 长打印机名称
- 驱动程序文件名
- 数据文件名
- 配置文件名
- 帮助文件名
- 语言监器名称（如果没有，请将其设置为 NULL）
- 默认数据类型（如果没有，将其设置为 NULL）
- 逗号分隔的附加文件列表

要配置打印机使用已上传的驱动程序之一，

```
$ rpclient -U printadmin -c ""
set driver \"myprinter\"\"Our Custom PS\" samba-server
```

# 30.8 调试 SAMBA

Samba 通常在运行时不需要不需要太多关注。然而，如果你遇到问题，可以参考两个主要的调试信息源：每个客户端的日志文件和 `smbstatus` 命令。确保你的配置文件中有适当的日志文件设置。

```
[global]
; %m 会为每个客户端创建一个单独写入的文件。
log file = /var/log/samba.log.%m
max log level = 1000
; 记录多少信息。你也可以为系统组件
; 设定日志级别（这里通常为 3，但认证级别为 10）。
log level = 3 auth:10
```

较高的日志级别会产生更多信息。记录需要时间，因此除非你正在调试，否则不要请求过详细的信息。操作可能会显著变慢。

以下示例显示了连接失败后紧接着成功时生成的日志。

```
[2009/09/05 16:29:45, 2] auth/auth.c:check_ntlm_password(312)
check_ntlm_password: Authentication for user [oetik] -> [oetik] FAILED
with error NT_STATUS_WRONG_PASSWORD
[2009/09/05 16:29:45, 2] smbd/server.c:exit_server(571)
Closing connections
```
