
```
humanresources          D   0 Tue Jul 13 23:57:36 1999
README                  261 Wed Jul 14 00:00:45 1999

33521 blocks of size 32768. 27022 blocks available
smb: \> quit
```

如你所见，我们能够使用 smbclient 命令连接到公共共享目录，并能够查看其中包含的目录和文件。

现在假设用户 tschenk 想将服务器上的主目录挂载到他的本地 Linux 客户端上。为此，他将使用 smbmount 和 smbumount 命令。

```
[tschenk@nomad tschenk]$ smbmount //quicksilver/tschenk -c 'mount -samba \
-u 500 -g 500'
Added interface ip=192.168.50.25 bcast=192.168.50.255 netmask=255.255.255.0
Server time is Wed Jul 14 00:14:57 1999
Timezone is UTC-5.0
Password:
Domain=[ALCHEMY] OS=[Unix] Server=[Samba 2.0.3]
security=user
```

```
[tschenk@nomad tschenk]$ cd samba
```

```
[tschenk@nomad samba]$ ls -l*
lilo-colors.tar.gz  limp_penguin_ai.zip  linux-1.3.0.tar.gz  ljf.quote
limp_penguin.ai    linux-1.0.tar.gz     linux-2.0.tar.gz    lodlin16.tgz
limp_penguin.eps   linux-1.1.0.tar.gz   linux-2.1.0.tar.gz
limp_penguin.jpg   linux-1.2.0.tar.gz   linux-2.2.0.tar.gz
```

```
[tschenk@nomad samba]$ cd ..

[tschenk@nomad tschenk]$ smbumount samba

[tschenk@nomad tschenk]$ ls samba
```

如你所见，用户 tschenk 能够将服务器上的共享主目录挂载到名为 samba 的目录上，然后再次卸载它。

## 注意

为了让普通用户以这种方式挂载和卸载共享，smbmount 和 smbumount 命令必须设置为 setuid root。对于 Samba 的 Red Hat RPM 来说，它们并非以这种方式安装。

作为最后一次测试，我们将尝试在连接到服务器的打印机上打印一个文件。为此，我们将再次使用 smbclient 命令。如图所示：

```
[tschenk@nomad tschenk]$ smbclient //quicksilver/lp -U tschenk%password \
-c 'print invite.ps'

Added interface ip=192.168.50.25 bcast=192.168.50.255 netmask=255.255.255.0
Domain=[ALCHEMY] OS=[Unix] Server=[Samba 2.0.3]
putting file invite.ps as invite.ps (average 383.479 kB/s)
```

如你所见，将 Linux 设置为 Windows 网络上的客户端并不困难，如果运气好，一切都会顺利进行。当然，如果你在尝试这里所示的任何示例时遇到问题，你可能在问自己，现在怎么办？幸运的是，Samba 包包含了一些可以帮助你诊断问题的文档。这些文档位于你的 Red Hat Linux 系统中的 /usr/doc/samba-2.0.3/docs。此外，Deja.Com 网站是一个寻求帮助的好地方。访问他们的网站并使用 Usenet 搜索引擎搜索关于 Samba 的新闻组信息，或向其中一个 Samba 新闻组发布你的问题。

## Linux 和 Samba 作为服务器操作系统

在你的 Windows 网络上，Linux 和 Samba 更有趣的角色是作为资源服务器。在前面描述的示例网络中，一个适合由 Linux 主机替换的良好候选者是共享公共目录、用户主目录和两台打印机的资源服务器。通过在此处替换 Linux 系统，你可以大幅节省网络成本，因为你不需要 NT 许可证。除了与网络其他部分共享资源外，你还可以使用该系统处理电子邮件、运行 DNS 服务器并为你的内联网设置 Web 服务器。你可以以更低的成本做到这一切，因为所使用的机器可以比等效的 NT 服务器弱得多。

## 设置 smb.conf 文件

资源服务器配置所需的 smb.conf 文件自然比之前的更复杂，正如你可能猜到的那样。以下是我在为本书测试 Samba 时使用的配置文件：

```
##=========================== Global Settings ===========================
[global]
workgroup = ALCHEMY
server string = Samba Server
hosts allow = 192.168.50. 127.
printcap name = /etc/printcap
```

```
load printers = yes
print command = lpr -P %p %s ; rm %s
log file = /var/log/samba/log.%m
max log size = 50
security = user
encrypt passwords = yes
smb passwd file = /etc/smbpasswd
socket options = TCP_NODELAY
dns proxy = no

#========================== Share Definitions ==========================

[homes]
comment = Home Directories
browseable = no
writable = yes
create mode = 0750

# NOTE: If you have a BSD-style print system there is no need to
# specifically define each individual printer
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest ok = no
writable = no
printable = yes

[public]
comment = Public Stuff
path = /home/samba
public = yes
writable = yes
printable = no
write list = @staff
```

此配置文件使我的 Samba 服务器上的所有打印机只要是有效用户就可以供网络使用。它还共享主目录以及 staff 组成员的公共空间。一旦创建此文件，需要重新启动服务器，并通过运行以下命令完成：

/etc/rc.d/init.d/smb restart

## 从 Windows 测试你的配置

对我的 Samba 服务器进行的首次测试中，我尝试从 Windows 98 客户端访问 Samba 服务器上的公共目录。为此，我以用户 tschenk 登录，该用户也在 Samba 服务器上存在，并单击了“网络邻居”图标。如图 17.9 所示，这就是我第一次成功迹象的地方。

图 17.9
显示我的 SAMBA 服务器的网络邻居窗口。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_522_0.png)

然后我单击了“整个网络”图标，并看到了图 17.10 所示的屏幕，其中显示我的 ALCHEMY 域已被识别。

图 17.10
显示 ALCHEMY 工作组的网络邻居窗口。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_522_1.png)

进一步深入，我看到了网络上实现 SMB 协议且对网络可见的主机（见图 17.11）。

图 17.11
显示 ALCHEMY 域中主机的网络邻居窗口。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_523_0.png)

我再次通过单击代表主机 Quicksilver 的图标进行深入，并看到了图 17.12 所示的屏幕，其中显示了我试图从 Samba 服务器共享的资源。

图 17.12
Quicksilver 共享资源。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_523_1.png)

最后一次深入显示，我确实成功共享了我在 smb.conf 文件中指定的资源。图 17.13 显示了公共目录的内容。

## 图 17.13

公共共享目录。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_524_0.png)

我的最后一次测试是查看是否可以向我的 Samba 服务器上的 lp 打印机打印。为此，我只需单击 lp 图标，经历配置对话框使用适当的驱动程序配置此打印机，然后打印测试页，结果正如预期一样正常工作。

自然地，一切如此顺利部分是运气使然。但这也是因为我花了大量时间阅读 Samba 附带的文档，以便了解 Windows 网络的行为方式，以及查阅 Samba 的手册页。

## Samba 帮助来源

如果你在设置 Samba 时运气不佳，仍然可以获得帮助，如果你礼貌地请求，甚至可能获得 Samba 开发人员的帮助。让我们看一下几个 Samba 帮助来源。

## Samba 邮件列表

有许多邮件列表涉及 Samba 的各个方面，从开发到支持。一些列表面向终端用户，也面向开发人员。表 17.4 是可用邮件列表的部分列表。

表 17.4 SAMBA 邮件列表

| 列表名称 | 讨论重点 |
|---|---|
| samba | Samba 软件套件的一般讨论。 |
| samba-announce | 新版本或其他 Samba 社区感兴趣事项的公告。 |
| samba-docs | 关于 Samba 文档项目的讨论。 |
| samba-technical | 开发人员关于 Samba 相关技术问题的讨论。 |

