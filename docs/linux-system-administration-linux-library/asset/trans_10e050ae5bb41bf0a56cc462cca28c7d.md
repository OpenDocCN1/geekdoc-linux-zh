

# 文件共享

程序将要求你输入两次密码。当你第一次运行此程序时，它可能会通知你找不到 `smbpasswd` 文件，并正在创建它。

如果你喜欢使用明文密码和标准的 Linux 密码数据库，可以通过更改任何 Windows 客户端以发送明文密码来实现。在 Red Hat 系统上，`7.0/usr/doc/samba-2.0/docs` 目录包含几个 `.reg` 文件，可以使用这些文件对 Windows 系统进行相应的更改。将与你运行的操作系统版本同名的文件（例如用于 Windows 98 的 `Win98_PlainPassword.reg`）拷贝到软盘，将其移动到目标 Windows 系统，并双击该文件以调整客户端配置。在更改生效之前，你需要重启电脑。

# 配置文件共享

文件共享占据了大多数 `smb.conf` 文件的大部分，特别是在具有许多共享的服务器上。此共享演示了常见的文件共享选项：

```
comment = Shared Program Directory
path = /home/samba/bigshare
read only = No
browseable = Yes
create mask = 0666
directory mask = 0777
```

此共享参数的含义如下：

- comment `comment` 参数的作用与服务器字符串（server string）参数相似，不同之处 `comment` 设置的是与特定共享关联的注释。

- path `path` 参数设置了要共享的目录。这可以是计算机上的任何目录，尽管出于安全考虑，共享某些目录（如 `/etc`）是不明智的。

- read only 默认情况下，Samba 不授予其共享目录的访问权限。你可以通过包含 `read only = No` 参数来允许用户写入 Samba 共享。`writable` 和 `read only` 是反义词，因此 `writable = Yes` 与 `read only = No` 是同义的。

# browseable

此参数如果设置为 `Yes`，将使共享显示在 Windows 的“网络邻域”浏览列表中。通常将此参数设置为 `Yes` 是最好的。

# create mask and ndirect mask

这些参数设置用户通过 Samba 创建的文件和目录的权限。例如，这些值被设置了较高的数值，以便所有用户都能读写彼此的文件。当然，你可能想要限制权限而不是扩展权限。默认值分别为 `0744` 和 `0755`。

有一个特殊的名称值得特别提到：`[homes]`。如果你使用此共享，应该省略 `path` 参数，Samba 会提供一个对应于用户家目录的共享。例如，如果 Jennie 登录服务器，该共享在客户端上显示为 `JENIE`，并显示用户的家目录文件。这种共享在用于存储单个用户文件（与共享打印机程序相反）的服务器上非常有用且流行。

除了文件共享外，Samba 还支持打印机共享，正如第 13 节所述的。启用打印机共享最简单的方法是创建一个 `[printers]` 共享，该共享应该设置 `print ok = Yes` 参数。这会导致 Samba 共享在 `/etc/printcap` 中定义的每个打印机队列。由于 Linux 打印机队列通常被定义为 PostScript 打印机，因此你应该在 Windows 客户端将它们视为 PostScript 打印机。

> 提示：Apple LaserJet 驱动程序通常在 Linux 上使用 Ghostscript 的打印机上运行良好。

# 使用 Samba 作为客户端

Samba 包含两个客户端：`smclient` 和 `smbmount`。第一个是一个允许你以类似于文本模式 FTP 程序的方式执行文件传输的程序。相比之下，`smbmount` 允许将共享挂载到 Linux 目录树上，你可以使用 `mount` 命令挂载 NFS 共享。（事实上，从 Samba 2.0.6 开始，你可以使用 `mount` 代替 `smbmount`。）这些包也有许多 GUI 前端，因此你可以像在 Windows 中一样，从 Linux 浏览 SMB/CIFS 网络。

所有 Samba 客户端程序都依赖于 `smb.conf` 中的 `[global]` 部分设置来控制操作的 NetBIOS 名称和计算机名称。在将 Samba 作为客户端之前，你应该确保这些功能设置正确。

要使用 `smclient`，你启动它并传递服务器名称以及你想访问的共享：

```
$ smclient //server/share
```

在你输入此命令后，`smclient` 会提示你输入密码，该密码应与服务器上的用户名匹配。（如果你的服务器上的用户名与客户端不同，你可以使用 `-U` 参数指定服务器上的用户名）。`smclient` 中可用的命令与文本 ftp 程序类似——`ls` 查看可用文件；`put` 和 `get` 分别向和从共享传输文件；`cd` 进入新目录；你可以输入 `?` 或 `help` 获取命令摘要。

尽管 `smclient` 是快速传输少量文件的好方法，但如果你想直接修改服务器上的文件，`smbmount` 更加灵活。要使用 `smbmount`，请以下格式执行命令：

```
$ smbmount //server/share /mountpoint
```

注意：如果以 root 使用 `smbmount` 命令，必须设置用户 ID (`uid`) root 才能工作：`smint`（smbmount 的助手）。如果你使用此共享，应该省略 `path` 参数，Samba 会提供一个对应于用户家目录的共享。例如，如果 Jennie 登录服务器，该共享在客户端上显示为 `JENIE` 并显示用户的家目录文件。这种共享在用于存储单个用户文件的服务器上非常有用且流行（与共享打印机程序相反）。

除了文件共享，Samba 还支持打印机共享，正如第 13 节所述。启用打印机共享最简单的方法是创建一个 `[printers]` 共享，该共享应该设置 `print ok = Yes` 参数。这会导致 Samba 共享在 `/etc/printcap` 中定义的每个打印机队列。由于 Linux 打印机队列通常被定义为 PostScript 打印机，因此你应该在 Windows 客户端将它们视为 PostScript 打印机。

如果以 root 使用 `smbmount` 命令，必须设置用户 ID (`uid`) root 才能工作：`smint`（smbmount 的助手）。如果你使用此共享，应该省略 `path` 参数，Samba 会提供一个对应于用户家目录的共享。例如，如果 Jennie 登录服务器，该共享在客户端上显示为 `JENIE` 并显示用户的家目录文件。这种共享在用于存储单个用户文件的服务器上非常有用且流行。

