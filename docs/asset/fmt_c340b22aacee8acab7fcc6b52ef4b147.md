
```
$ smbclient //cleopatra\public -User1$secret -c backup.tar samba-updates
added interface ip=192.168.1.200 bcast=192.168.1.255 nmask=255.255.255.0
Domain=[NILE] OS=[Windows NT 4.0] Server=[NT Lan Manager 4.0]
directory=\samba-updates
50732 (1651.3 kb/s) \samba-updates\network-arch.jpg
12800 (1250.0 kb/s) \samba-updates\network-arch.ppt
5899 (5760.7 kb/s) \samba-updates\ForSambaHOWTO.doc
406016 (15860.0 kb/s)
tar: dumped 5 files and directories
Total bytes written: 47184
```

可以恢复文件：

```
$ smbclient //cleopatra/public -User1$secret -c x backup.tar
added interface ip=192.168.1.200 bcast=192.168.1.255 nmask=255.255.255.0
Domain=[NILE] OS=[Windows NT 4.0] Server=[NT Lan Manager 4.0]
directory=\samba-updates
50732 (1651.3 kb/s) \samba-updates\network-arch.jpg
12800 (1250.0 kb/s) \samba-updates\network-arch.ppt
5899 (5760.7 kb/s) \samba-updates\ForSambaHOWTO.doc
406016 (15860.0 kb/s)
tar: dumped 5 files and directories
```

Samba 还包含一个专门设计用于方便备份的包装脚本，`smbtar` 脚本安装在 `/usr/local/samba/bin`。详情请参阅 `smclient(1)` 页。

## 打印文件

将文件打印到 CIFS 服务器类似于将文件上传到磁盘。首先，我们将以匿名用户身份连接到 `COLOR` 共享。

```
$ smbclient //cleopatra/color -User1$secret
added interface ip=192.168.1.200 bcast=192.168.1.255 nmask=255.255.255.0
Domain=[NILE] OS=[Windows NT 4.0] Server=[NT Lan Manager 4.0]
smb: >
```

接下来，我们将切换到文件所在的本地目录（例如 `~/Documents`）。由于 `smbclient` 无法处理波浪号 (~) 扩展或目录路径环境变量，因此我们必须输入绝对路径。

```
smb: > lcd /home/pogo/Documents
the local directory is now /home/pogo/Documents
```

我们将使用 `print` 命令将文件发送到打印机。

```
smb: > print resume.ps
putting file resume.ps as resume.ps (303.0 kb/s) (average 303.0 kb/s)
```

由于 `smbclient` 不支持在发送之前过滤文件的概念，文件应该是打印机可以理解的格式。常见格式包括 Postscript 或 PCL。这意味着你对所连接的打印机有一定的了解。

我们可以通过执行 `queue` 命令来验证文件是否已提交到打印机。

```
smb: > queue
2 234594 Remote Downlevel Document
```

这并没有提供关于打印队列文件中许多信息。在这种情况下，显示的文件名也是正确的。然而，我们可以验证文件大小以确保文件已溢出到打印机。

## Smbprint 脚本

`smbprint` 工具是随 Samba 提供的一个简单 shell 脚本，允许 Unix 系统打印到其他 CFS/SMB 服务器上的打印机。`smbprint` 利用 `smclient` 的命令行功能和能力来处理 STDIN，以便在一个简单的管道中处理要打印的文件。例如：

```
(
echo translate
echo print -
cat
) smbclient "$server/$service" -U user$pass
```

这种语法与 `smbprint` 使用的不完全相同，但它说明了相同的原理。

- 在子 shell 中，两个 `echo` 语句告诉 `smclient` 翻译所有输入并从 STDIN 打印 (-)。我们在子 shell 中（括号内）执行这些命令，以便通过 STDIN 向 `smbprint` 发送命令流。
- `cat` 命令将 STDIN 复制到 STDOUT，但 STDOUT 连接到管道的下一个阶段，而 STDIN 连接到要打印的文件。
- `smbclient` 运行，连接到 `$server` 中指定的服务器，并使用 `$service` 中指定的服务（`$server` 和 `$service` 是由 `smbprint` 设置的），使用传递给它的其他参数，并处理 STDIN。
- 然而，由于 STDIN 连接到上述的子 shell，它依次接收了 `translate` 命令、然后是 `print -` 命令，最后是待打印的文件，所有内容都在 STDIN 上。

### Unix 的 CIFS 客户端 209

`lpd`。此命令在在前两个命令执行的子 shell 中也会执行。

- `smbclient` 运行，连接到 `$server` 中指定的服务器，并使用 `$service` 中指定的服务（`$server` 和 `$service` 是由 `smbprint` 设置的），使用传递给它的其他参数，并处理 STDIN。
- 4. 然而，由于 STDIN 连接到上述的子 shell，它依次接收了 `translate` 命令、然后是 `print -` 命令，最后是待打印的文件，所有内容都在 STDIN 上。

## 从 Unix 打印到 Windows

从你的 Unix 服务器打印到连接到 Windows 客户端的打印机通常非常有用。可以通过使用适当版本的 `smbprinttool` 作为打印过滤器来实现。我们将介绍如何针对伯克利风格的打印（LPD、PLP 和 LPRNG）以及 System V 风格的打印进行操作。

Samba 自带了一个名为 `smbprint` 的小 shell（用于 BSD 版本）和 `smbprint.sysv`（用于 System V 系统）。如前所述，该程序接受打印作业并将它们排队到远程 Windows 系统共享的打印机上。配置这些项的步骤取决于你的 Unix 系统使用的是 BSD 风格打印还是 System V 风格打印。无论何种，打印机必须位于 Windows 机器。如果 Windows 主机安装了“网络文件和打印机共享”服务（Windows NT/2000 客户端启用此功能），只需从 Windows 属性中选择共享选项并启用启用功能即可——这就是全部的操作。图 12.3 显示了如何从 Windows 98 系统打印打印机。

![](img/e6dc04fe420c61acdd193e83a4772)

## 使用 BSD 风格打印到 Windows

BSD 风格打印使用 `LPD` 并由文件 `/etc/printcap` 控制。所有打印机都定义在 `printcap` 中。关于配置远程 LPD 打印机的完整细节，参考 `printcap` 是一个好主意。要指定特定打印机将其作业发送到远程 Windows 系统上的共享打印机，请执行以下步骤：

1. 定义打印机；即手动或使用你喜欢的工具构建 `printcap` 条目。
2. 在为打印机创建的池化目录中（通常为 `/var/spool/<printer-name>`），创建一个文件（确保文件名以点开头）并放置以下几行：

```
server=<server name>
service=<printer share>
password=<password>
```

3. 将你的打印机 `printcap` 条目中的过滤器更改（或添加）为 `<smbprint 所在的目录路径>`：
4. 重启打印机。

对于远程服务器 `HAWK` 提供的名为 `MYPRINTER` 的命名打印机，且访问不需要密码，文件将如下：

```
server=HAWK
service=MYPRINTER
password=""
```

![](img/e6dc04fe420c61acdd193e83a4772)

对于位于 Windows NT 系统上的打印机，可以使用 Windows TCP/IP 打印服务并在 NT/2000 上安装 `LPD`。

## 使用 System V 风格打印到 Windows

System V 风格打印与 BSD 风格不同并使用 IP。Samba 支持使用位于 Samba 树 `examples/printing` 目录下的 `smbprint.sysv` 脚本从 System V 系统打印到 Windows 。该脚本是 BSD 风格脚本的修改版本。要使用它，需要对脚本进行修改以指定 Windows 服务器、服务和密码。这些位于程序中的一个块中：
