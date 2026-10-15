
# 第 9 章 基础 TCP/IP 工具

## w2kserver

```
Connected to w2kserver.book.local.

220 w2kserver Microsoft FTP Service (Version 5.0).

Name (w2kserver:root): ftp

331 Anonymous access allowed, send identity (e-mail name) as password.

Password:

230 Anonymous user logged in.

Remote system type is Windows_NT.

ftp> get boot.txt

200 PORT command successful.

150 Opening ASCII mode data connection for boot.txt(37064 bytes).

226 Transfer complete.

37064 bytes received in 0.03 seconds (1431.72 Kbytes/s)

ftp>
```

然而，如果你从 HP-UX 连接到另一个 UNIX 系统，你的默认传输模式是 BINARY（二进制）。同样，以下输出验证了这一点：

```
# ftp hpux1

Connected to hpuxi.book.local.

220 hpuxi.book.local FTP server (Version 1.1.214.5 Tue Nov 16 09:39:15 GMT 1999).

Name (hpuxi:root): root

331 Password required for root.

Password:

230 User root logged in.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp>
```

## 9.4 Tftp

简单文件传输协议 (Tftp) 提供了一种将系统配置为不需要身份验证的 FTP 服务器的方法。对于这项工作，用户需要知道 Tftp 服务器的名称以及要检索的文件名（没有 Tftp 目录列表），仅此足够了。Tftp 服务器配置了一个名为`tftp`的用户，其主目录是用于放置或检索文件的仓库。Windows 2000 没有 Tftp 服务器；它仅有客户端。

### 9.4.1 配置 HP-UX Tftp 服务器

在 HP-UX 上配置 Tftp 的最简单方法是使用 SAM。运行 SAM，选择“网络和通信”→“网络服务”（见图 9–8）。如果 Tftp 被禁用，请从菜单栏中选择“操作”并选择“启用”。

通过这种方式配置 Tftp 会执行以下操作：

- 创建一个名为`tftp`的用户，其密码已禁用，主目录为`/home/tftpdir`。该目录已分配了正确的所有者和权限。更多信息请参阅`man tftp`。
- 确保在`/etc/inetd.conf`中启用了 Tftp。

![](img/1c1e7552b53cca888836b6c6895bdb48_151_0.png)

9-8 使用 SAM 启用 Tftp。

如果你想授予远程系统通过 Tftp 获取文件的权限，则该文件必须对`tftp`用户可见。如果你想授予远程系统通过你的系统 Tftp 传输文件，则该文件必须存在且允许`tftp`用户写入。

### 9.4.2 运行 Tftp

Windows 2000 Tftp 客户端的语法为：

```text
tftp [-i] host [get | put] source [destination]
```

此客户端没有交互模式。因此，你必须指定你是在执行`get`还是`put`操作，以及你想要传输的文件。（`get`或`put`参数是必需的，也是可选的。）

## 9.5 Rsh 和 Rcp

（注：此处原文文本存在重复和错误，已根据逻辑处理翻译。）

### 9.5.1 运行 Rsh

（注：此处原文文本存在重复和错误，已根据逻辑处理翻译。）

### 9.5.2 示例

查询`hpux`上上次系统启动的时间。

```text
D:\>rsh hpux -l dylan -b

   system boot Oct 24 18:39
```

```bash
find: cannot open /var/adm/sw/save
find: cannot open /var/adm/sw/save_custom
find: cannot open /var/spool/uucp/.Corrupt
find: cannot open /var/spool/uucp/.Sequence
find: cannot open /var/spool/uucp/.Workspace
find: cannot open /var/spool/uucp/.Qxtdir
find: cannot open /tmp/.AgentSockets
find: cannot open /usr/newconfig/etc/sam/custom
find: cannot open /.dt/Desktop
/etc/rc.log
/etc/auto_parms.log
/var/opt/ignite/local/install.log
/var/opt/dce/dce/config/dce_config.log
```

上述输出中的 " " 表示输出内容多于我想要的内容。在该命令中，我指定了用户`dylan`，这是一个非特权用户。因此，当该用户尝试查看`root`以外用户的目录权限时，我的`find`命令返回了错误信息。为了消除这些错误信息，我可以将错误重定向（在 UNIX 系统中指定为文件描述符 2）到`/dev/null`，即垃圾桶。记住，我必须引用重定向符号，因为 Windows 2000 上没有`/dev/null`：

```cmd
D:\>rsh hpux1 -l dylan find -name "*.log" 2> /dev/null

/etc/rc.log
/etc/auto_parms.log
/var/opt/ignite/local/install.log
/var/opt/dce/config/dce_config.log
/var/opt/dce/dced/dced.log
/var/opt/dce/svc/fatal.log
/var/opt/dce/svc/error.log
```

如果我想将此文件列表复制到 Windows 2000 文件，命令如下：

```cmd
D:\>rsh hpux1 -l dylan find -name "*.log" 2> /dev/null 

c:\windows\temp\hpux1_log_files.txt
```

该命令实际上是一行，但为了显示方便进行了分行。

### 9.5.3 运行 Rcp

`Rcp`允许你将文件复制到本地 Windows 2000 系统或其他运行`rshd`或`remsh`的系统。你可以将整个目录结构从一个系统复制到另一个系统。Windows 2000 `Rcp`的帮助开关显示如下：

```text
rcp [-a | -b] [-h] [host][.user:]source [host][.user:]path]destination
```

- `-a` 指定 ASCII 传输模式。此模式将 EOL 字符转换为 UNIX 的换回符，以及个人计算机的换回符/换行符。这是默认的传输模式。
- `-b` 指定二进制镜像传输模式。
- `-h` 传输隐藏文件。
- `-r` 复制所有子目录的内容；目标必须是一个目录。
- `host` 指定本地或远程主机。如果`host`指定为 IP 地址或名称中包含点，则你必须指定用户。
- `user` 指定要使用的用户名，而不是当前用户名。
- `source` 指定要复制的文件。
- `path\destination` 指定相对于远程主机登录目录的路径。在远程路径中使用转义字符（`\`、`"` 或 `?`）可以在远程主机上使用通配符。

让我们使用一些示例来澄清。

我以用户`dylan`的身份登录 Windows 2000。我的主目录是`C:\Documents and Settings\dylan`。在我的 HP-UX 系统上，我有一个`dylan`账户，主目录为`\home\dylan`。在这种情况下，为了将我的 Windows 2000 主目录中名为`CHAPTER.DOC`的文件复制到 HP-UX 主目录，我将输入：

```cmd
C:\Documents and Settings\dylan-rpc CHAPTER.DOC hpux1:dylan
```

微软文档建议，简单地输入`rcp CHAPTER.DOC hpux1`就足够了。然而，我的测试显示，这样做只会将`CHAPTER.DOC`复制到名为`hpux1`的本地文件中。因此，我必须指定`hpux1:dylan`作为目标和用户名。

要复制 Windows 2000 主目录（也是当前目录）中的所有文件：

```cmd
```

