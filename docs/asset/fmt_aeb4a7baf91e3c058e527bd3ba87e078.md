
;

;/etc/smb.conf

;

; Debian GNU/Linux Samba 软件包的示例配置文件

;

![](img/f36419c0b225d12fa66de83fa271829b_624_0.png)

### 列表 18.1 续

; 请参阅 `smb.conf` 的手册页以获取每个参数的详细描述。

```
[global]
printing = bsd
printcap name = /etc/printcap
load printers = yes
guest account = nobody
invalid users = root
```

; "security = "user" 始终是一个好主意。这将要求每个访问服务器的用户在服务器中都有一个 UNIX 账户。

; security = user

; 修改此项以适用于你的 Samba 服务器所在的工作组。

; workgroup = WORKGROUP

```
server string = %h server (Samba %v)
```

; 根据我所知，这些套接选项在 Linux 下确实可以加快 Samba 的速度。

; socket options = IPTOS_LOWDELAY TCP_SO_SNDBUF=4096 SO_RCVBUF=-4096

; 密码默认是加密。这意味着最新的 Windows 95 和 NT 客户端可以毫无问题地连接到 Samba 服务器。

; encrypted passwords = yes

; 使用 WINS 服务器始终是一个好主意。如果你想让此服务器成为网络的 WINS 服务器，请将以下参数更改为 "yes"。否则，保持为 "no" 并在下方指定你的 WINS 服务器（注意：只能有一个服务器作为 WINS 服务器）。

; 更多信息请阅读 BROWSING.txt。

wins support = no

- ; 如果此服务器不是 WINS 服务器，请指定谁是 WINS 并取消下一行的注释。

; wins server = 172.16.0.10

- ; 请阅读 BROWSING.txt 并根据你的网络设置接下来的四个参数。没有有效的默认值，因此它们被注释掉了。

; os level = 0

; domain master = no

; local master = no

; preferred master = no

- ; 我们应该使用什么命名服务以及按什么顺序将主机名解析为 IP 地址？

; name resolve order = lmhosts hosts bcast

这可以防止 `nmbd` 通过 DNS 搜索 NetBIOS 名字。

dns proxy = no

; 名字大小写转换选项

```
preserve case = yes
short preserve case = yes
```

; 这个布尔参数控制当 `/etc/smpasswd` 文件中的加密 SMB 密码更改时，Samba 是否尝试同步 UNIX 密码与 SMB 密码。
unix password sync = false

; 为了在 Debian GNU/Linux 系统上实现 UNIX 密码同步，必须设置以下参数（感谢 Tulus 的指点）：
passwd program = /usr/bin/passwd * %n%n
passwd chat = *New:password:* %n%n*Re-enter:%s*newpassword:* %m %s
*Passwordchanged.

; 只有在你安装了 linopup 软件包时，以下参数才有用。Samba 维护者和 linopup 维护者正在努力简化 linopup 和 samba 的安装与配置。
message command = ; 只有在你安装了 linopup 软件包时，以下参数才有用。Samba 维护者和 linopup 维护者正在努力简化 linopup 和 samba 的安装与配置。
message command = /usr/bin/passwd

## 使用 Samba 与微软网络

```
[global]
printing = bsd
printcap name = /etc/printcap
load printers = yes
guest account = nobody
invalid users = root
```

```
[homes]
comment = Home Directories
browseable = no
```

### 列表 18.1 续

```
[global]
printing = bsd
printcap name = /etc/printcap
load printers = yes
guest account = nobody
invalid users = root
```

```
[printers]
comment = All Printers
browseable = no
```

# 使用 Windows 客户端进行测试

Samba 让 Linux 计算机出现在 Windows “网络邻居”中。网络邻居中显示的是 Samba 服务器 `/etc/smb.conf` 文件中 `[global]` 部分 `workgroup` 关联的工作组名称。Samba 支持全大写、8 个字符以内且绝对不包含空格的工作组名称。这是 Windows 的局限性。

接下来，在 `[global]` 部分，临时取消注释（即移除行前的注释字符，从而激活该选项）`password level` 和 `username level`。将 `password level` 设置为此系统上可能的最长用户名，将 `username level` 也设为可能的最长用户名 (uid)。（等等，原文写的是“username level the longest likely username (uid)”）。）。这些设置指定了有多少个字符是不区分大小写的，这对于像 Windows 这样不区分大小写的 SMB 客户端非常重要。

> 注意
>
> 通常不需要更改 `username level` 和 `password level`。之前的建议仅仅是为了临时消除任何可能的大小写敏感问题。当系统运行正常时，你应该重新恢复 `password level` 和 `user level` 的注释。

每当遇到用户和密码的大小写敏感相关的故障排除问题时，你可以再次取消它们的注释，并在解决后恢复它们。

# 加密密码与明文密码

现在你必须决定是使用明文密码还是加密密码，以及如何实现这一决定。早期的 Windows SMB 客户端默认使用明文密码。从 Windows 95 OEM Service Release 2 开始，Windows 默认使用加密密码。所有的 Windows 98 客户端都默认加密。同样，在 Windows NT 4.0 Service Pack 3 中，默认行为也从明文变为加密。网络上的所有客户端必须使用相同的方案，或者如果你的任何客户端不支持加密密码（例如，如果你有 Windows for Workgroups 客户端），则你必须使用明文密码。

在 Debian GNU/Linux 2.1 默认的 `smb.conf` 中，启用了加密密码，因此对于 95-SR2 之前的 Windows 版本或 4.0 Service Pack 3 之前的 NT 版本，每个明文客户端都必须改为加密密码，或者必须更改服务器的 `smb.conf` 以禁用加密密码，并将任何加密密码的客户端改为使用明文密码。

## 注意

Debian 2.1 随附的文档包含了关于明文与加密密码及其影响的详细讨论。请查看：

`/usr/doc/samba-doc/Win95.txt`

`/usr/doc/samba-doc/WinNT.txt.gz`

`/usr/doc/samba-doc/ENCRYPTION.txt.gz`

Windows NT 用户：NT SMB 客户端带来了额外的挑战。如果你在使用 Windows NT SMB 客户端遇到问题，务必仔细阅读这三个文档。

注意注意以 `.gz` 结尾的文件是使用 `gzip` 程序压缩的。要查看这些文档，可以使用如下命令：

```
zcat /usr/doc/samba-doc/ENCRYPTION.txt.gz | less
```

# 禁用和启用密码

要在服务器中禁用加密密码，请编辑 `smb.conf` 文件。在 `[global]` 部分，注释掉 `encrypt passwords = yes` 和 `smb password file = /etc/passwd` 这行。

要在客户端中启用加密密码，启动注册表并导航到 `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VXD\NETUPS`。如果它包含一个名为 `EnablePlainTypeText` 的对象，将该对象的值设置为 0。如果不包含该对象，则创建一个 DWORD 类型的对象，并赋值为 0。退出 `regedit` 并重启 Windows 机器。

与 MIS 网络进行交互

使用 SAMBA

# 警告
