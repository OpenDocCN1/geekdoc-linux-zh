
记住，这些主机中的任何一个可能是运行在 Linux 或 Solaris 上的 Samba 服务器，而 Microsoft Windows 服务器和客户端使用的是原生 SMB 网络。你可以使用以下命令启动 `nmbd` 守护进程：

```
/usr/local/samba/bin/nmbd -D
```

`-D` 选项指定 NetBIOS 名称服务守护进程作为独立守护进程运行，而不是通过互联网超守护进程 `inetd`。

## Samba 客户端

有多种方法可以与 Samba 服务器建立连接。如果你位于 NT 工作站或类似设备上，Solaris 服务器应该直接显示为普通的 NT 服务器，各个文件系统将列列为共享（由 `smb.conf` 文件决定）。此外，Solaris 文件系统可以被映射为本地 NT 驱动器。这使得 Solaris Samba 成为为多个工作站提供可靠文件服务的理想解决方案。

Linux 用户可以使用 `smount` 命令挂载共享的 Solaris 文件系统，以保持文件共享的单一协议，而不是（例如）使用 Solaris 服务器 SYDNEY 上的 `answerbook`，你可以在 Linux 系统上执行以下命令：

```
# smount //SYDNEY/answerbook /usr/local/answerbook
```

这将远程的 `answerbook` 共享挂载到挂载点 `/usr/local/answerbook` 的本地文件系统上。当然，在使用此命令挂载之前，需要先创建挂载点：

```
# mkdir -p /usr/local/answerbook
```

在不再需要该共享时卸载它，你可以使用以下命令：

```
# smbount /usr/local/answerbook
```

希望访问远程 Samba 共享（来自 Solaris、NT 或 Linux 服务器）的 Solaris 用户通常使用 `smclient` 程序，它从命令行运行，并有一组类似于 FTP 的简单命令集。`smclient` 提供了一种非常实用且紧凑的方法，用于在远程服务器上上传、下载和删除文件。要建立初始连接，可以使用如下的命令：

```
# smclient -L system
```

其中 `system` 是远程 Samba 服务器的名称。要确定 SYDNEY 服务器上有哪些共享，你可以使用此命令：

```
# smclient -L SYDNEY
Added interface ip=62.12.48.43 bcast=62.12.48.43 nmask=255.255.255.0

Domain=[EASTUS] OS=[Unix] Server=[Samba 3.0.6]
```

```
Sharename      Type        Comment
----------      ------
answerbook    Disk        Sun Answers
homes         Disk        User Directories
IPC$           IPC         Service (Samba 3.0.6)
```

```
Server         Comment
-------        --------
SYDNEY         Samba 3.0.6
Workgroup      Master
EASTUS         WGONG
```

要连接到共享 `//SYDNEY/answerbook`，使用以下命令：

```
# smclient
```

`smclient` 提供了自己的 shell，因此你可以使用表 31-1 列出的命令列出目录内容、切换目录以及上传和下载文件。

使用 Samba 访问远程打印机略有不同：必须向 `smclient` 命令提供 `-P` 选项以识别目标共享。例如，要挂载 SYDNEY 上名为 `hp` 的打印机，你需要使用：

```
$ smclient -P //SYDNEY/hp
```

| 表 31-1 命令 | 操作 |
|---|---|
| smclient <dir> | 切换目录 |
| dir <dir> | 显示目录 |
| get <file> | 从服务器获取单个文件 |
| ls <dir> | 显示目录 |
| mget <file> | 从服务器获取多个文件 |
| mput <file> | 向服务器存储多个文件 |
| put <file> | 向服务器存储单个文件 |

## 配置 Samba 守护进程

全局部分定义了几个影响 `smbd` 运行的关键参数，包括工作组名称（EASTAUS）、本地服务器名称（SYDNEY）、标识系统的字符串（Solaris Samba 3.0.6）、主接口地址（62.12.48.43）、安全级别（standard）、Samba 日志路径（/usr/local/samba/）以及来客帐户名称（guest）。一个示例的 `smb.conf` 如下：

```
[printers]
comment = SYDNEY HP Printer
path = /var/spool/hp
print ok = Yes
browseable = Yes
[homes]
comment = User Home Directories
read only = No
browseable = Yes
[answerbook]
comment = Sun Answer Docs
path = /usr/answerbook/
guest ok = Yes
```

Samba 功能之一是配置检查程序 `testprogram`。`testprogram` 会启动 Samba 服务之前提醒任何配置错误。此外，`testprogram` 会打印与系统相关的所有 Samba 参数以及每个共享的参数，而不仅仅是 `samba.conf` 中显式声明的：

```
$ testprogram
Load samba config files from /usr/local/samba/lib/smb.conf
Processing section "[printers]"
Processing section "[homes]"
Processing section "[answerbook]"
Loaded service files OK.
WARNING: You have some share names that are longer than 8 chars
These may在浏览时产生错误，或者某些旧客户端无法访问。
按回车键查看你的服务定义 dump
# Global parameters
```
[global]
workgroup = EASTAUS
netbios name =
netbios aliases =
server string = Samba 3.0.6
interfaces =
bind interfaces only = No
```

# 642 第六部分：服务、目录与应用程序

```
security = USER
encrypt passwords = Yes
update encrypted = No
allow trusted domains = Yes
hosts equiv =
min passwd length = 5
map to guest = Never
null passwords = No
password server =
[printers]
comment = SYDNEY HP Printer
path = /var/spool/hp
print ok = Yes
browseable = Yes
```

```
[homes]
comment = User Home Directories
read only = No
browseable = Yes
```

```
[answerbook]
comment = Sun Answerbook Docs
path = /usr/answerbook/
guest ok = Yes
```

## Samba 守护进程状态

当 Samba 服务器在端口 139 上启动后，可以使用 `smbstatus` 命令可以轻松地跟踪服务器状态：

> $ smbstatus

这将返回一个所有当前通过本地 Samba 系统访问数据的客户端列表：

| Samba 版本 3.0.6 | | | | |
| 服务 | uid | pid | 机器 | 时间 |
| answerbook | root | 344 | MELBOURNE | Wed Nov 1 10:45:00 2000 |
| homes | root | 345 | MELBOURNE | Wed Nov 1 10:45:00 2000 |
| homes | steve | 1023 | HUNTER | Thu Nov 2 00:15:34 2000 |
