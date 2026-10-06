

# 远程文件访问

smbclient 允许你通过命令行混合 UNIX/FTP 客户端界面访问 Windows 服务器或 Samba 服务器上的文件。
若要进行最直接的用法，你只需运行以下命令即可：

```
# smbclient //server/share_name
```

在这里，server 是你想要连接的服务器名称（或 IP 地址）。在默认情况下，Samba 会自动将所有用户的家目录设置为共享。例如，用户 yang 可以通过浏览 `//fedora-server/yyang` 来访问她在名为 `fedora-server` 的服务器上的家目录。

> 注意 smbclient 命令中使用的 `/`（正斜杠）字符的方向，它用于指定 `server_name` 和 `share_name`！如果你习惯在 Windows 环境下进行类似的操作，你可能会使用 `\`（反斜杠）字符。

以下是一些你在连接服务器时可能需要配合 smbclient 使用的命令行参数：

| smbclient 参数 | 描述 |
| --- | --- |
| -I destIP | 你想要连接的目标地 IP 地址。 |
| -U username | 你想要以哪个用户身份连接。这将代替你当前登录的用户。 |
| -W name | 将工作组名称设置为 name。 |
| -D directory | 从目录开始。 |

一旦连接成功，你就可以使用 `cd`、`dir` 和 `ls` 命令浏览目录。你还可以使用 `get`、`put`、`mget` 和 `mput` 来来回传输文件。在线帮助详细说明了所有命令。只需在提示符处输入 `help` 即可查看可用命令。

> 如果你的服务器有基于主机或基于网络的防火墙保护，不要忘记开启必要的端口，以允许外部系统访问运行在你服务器上的 Samba 服务。
在 Fedora 等使用 `firewalld` 的类 Hat 系统上，你可以通过运行以下命令临时在主机防火墙上打开一个洞：

```
# firewall-cmd --add-service=samba
```

而在使用 Uncomplicated防火墙 (UFW) 方法管理主机防火墙规则的 Ubuntu 等类 Debian 系统上，你可以运行：
$ sudo ufw allow Samba

# 第 24 章节 Samba 635

让我们尝试连接到之前创建的共享（samba-share）。为了演示这一过程，连接将从一个不同的名为 client 的托管主机发起。

我们将使用 `smbclient` 工具连接到服务器，通过指定 `-U` 选项以访客身份连接。连接后，我们将进入一个 smb shell，提示符显示为：> 

在连接期间，我们将使用 `ls` 命令列出共享中可用的文件。然后，我们将尝试使用 FTP 管道命令 `get` 下载共享中的其中一个文件。

最后，我们将使用 `quit` 结束连接。这里是 clientB 连接到主机 server 的示例会话：

```
[root@clientB #] smbclient -U% //serverA/samba
Domain=[MYGROUP] OS=[Windows *] Server=[Samba 4.*]
smb: \> ls
      D      0      Sun 15 15:27:2020
              D      0      Sun 15 15:27:2020
foool      A      0      Sun 15 15:27:2020
fo2      A      0      Sun 15 15:27:2020
moo3      A      0      Sun 15 15:27:2020
  59501 blocks of size 8192. 55109 blocks available
smb: \> get foo2
getting file [foo2 of size 0 as foo2 (0.0 Kilobytes/sec) (average 0.0 Kilobytes/sec)
smb: \> quit
```
获取文件 [`foo2`（大小为 0，以 `foo2` 命名（0.0 Kilobytes/sec）（平均速度 0.0 Kilobytes/sec））
smb: \> quit

该文件 `foo2`（大小为 0）从 serverA 到 clientB 挂载的 Samba 共享。

> 注意：在 Fedora 等类 Hat 发行版中，你可以临时将 SELinux 设为允许模式以消除问题。
# setenforce 0

# 挂载 Samba 共享

如果你的内核支持 Samba（如现代 Linux 内核），你可以使用 `mount` 命令在本地文件系统上安全地挂载 Samba 共享。

1. 在本地系统上创建一个挂载点：
```bash
[root@server ~] mkdir -p /mnt/samba
```

2. 使用 `mount` 命令挂载共享：
```bash
[root@server ~] mount -t cifs //serverA/samba-share /mnt/samba -u guest
```

现在，你可以通过 `/mnt/samba` 目录访问 serverA 上的共享了。

# 允许空密码

如果你需要允许用户没有密码（尽管这是一个坏主意，但在某些情况下可能有合理的理由），你可以通过以下方式来实现：

使用 **pdbedit** 程序配合 `-c` 选项设置 Samba 用户：

```bash
# pdbedit -c '[N]' username
```

在这里，*username* 是你想要设置为空密码的用户名称。例如，为了允许用户 yyang 使用空密码访问 Samba 服务器，输入以下命令：

```bash
[root@server ~] pdbedit -c '[N]' yyang
```

