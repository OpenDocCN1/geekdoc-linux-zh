

## SAMBA 文档

最近的 SAMBA 镜像站点可以通过浏览 http://www.samba.org 来定位。你将发现以下在配置 SAMBA 时有用的指南：

- 保持简单。不要做不必要的事情，否则你只是在浪费时间。让 Windows 2000 提供它被设计来提供的服务。你应该使用 Windows 2000 服务器来提供 WINS 和浏览服务；除非你很勇敢，否则不要使用 SAMBA 来替代原生的 Windows 2000 服务。
- 尽可能使用 SAMBA 的内置共享功能。你不想每次添加/删除用户或打印机时都编辑你的 smb.conf 文件。使用 homes 和 shares 部分使你的 UNIX 主目录和打印机可供你的 NetBIOS 客户端使用。

以下是一个示例 smb.conf 文件：

```
# ======================== Global Settings ========================
[global]
netbios name = <SERVER_NAME>
workgroup = <WORKGROUP/DOMAIN NAME>
server string = Samba %v Server

browseable = yes

hosts allow = 192.168.1. 192.168.2.
hosts deny = 192.168.3. 192.168.4.

load printers = yes
printcap name = /etc/printcap
printing = bsd

log file = /var/log/samba/log.%m
max log size = 50

security = server
password server = <PDC_NAME>

username map = /etc/smbusers
domain group map = /etc/smbgroups

encrypt passwords = no

socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192

local master = no
domain master = no
preferred master = yes
os level = 0

name resolve order = wins lmhosts bcast
wins support = no
wins server = 192.168.1.10
wins proxy = no

lm announce = false

dns proxy = no

# ------------------- Share Definitions -------------------
[homes]
comment = Home Directory for %U
browseable = no
guest ok = no
writable = yes

[tmp]
comment = Temporary file space
path = /tmp
read only = no
public = yes

[printers]
comment = All printers in /etc/printcap
path = /var/spool/samba
printable = yes
```

那么这一切意味着什么呢？好吧，如果你适当地设置名称，你将能够从域中任何 Windows 机器访问所有主目录和打印机，以及 /tmp。SAMBA 服务器将针对你的域控制器对连接进行身份验证。由于这一次看可能有点令人困惑，我们将解释一些各个部分以及这些部分中的变量，这样你就能更好地理解我们在这里做什么。

[global] 部分包含控制 SAMBA 服务整体配置的设置。此部分指定你的服务器的身份，并且可以设置在其他部分中使用的许多默认值。表 8.10 描述了在 [global] 部分中使用的一些变量。

[homes] 部分，如果定义，则允许 SAMBA 在请求时动态共享用户的主目录，例如当尝试连接到 `\\server\username` 时。此部分为所有动态创建的主目录共享设置默认值。表 8.11 描述了在 [homes] 部分中使用的一些变量。

[printers] 部分，如果定义，则允许 SAMBA 从本地 /etc/printcap 配置文件创建打印机共享。此部分为所有动态创建的打印机共享设置默认值。表 8.12 描述了在 [printers] 部分中使用的一些变量。

| 变量 | 值 | 描述 |
| --- | --- | --- |
| netbios name | 文本 | 这个名字（没有双关语）本身就说明了一切。此参数指定 SAMBA 服务器将在 NetBIOS 网络上广播的名称。最好将此名称与你的 DNS 主机名保持一致。 |
| workgroup | 文本 | 指示 SAMBA 服务器将属于哪个 NetBIOS 网络。没有域名的选项；此选项涵盖两个领域。 |
| server string | 文本 | 这相当于 Windows 机器的描述。使用此行提供对你的 SAMBA 服务器更有意义的描述。 |
| browseable | yes/no | 这为所有服务设置默认浏览选项。简而言之，此选项决定服务器是否向网络进行广告。我们建议将此变量设置为 yes。 |
| hosts allow | 逗号分隔列表 | 指定允许访问你的 SAMBA 服务器的 IP 地址（或子网）列表。 |
| hosts deny | 逗号分隔列表 | 指定不允许访问你的 SAMBA 服务器的 IP 地址（或子网）列表。 |
| load printers | yes/no | 指定在启动 SAMBA 服务时是否加载你的 SAMBA 服务器上的打印机。 |
| printcap name | 路径名 | 指定查找加载打印机的 printcap 文件的位置。 |
| printing | AIX \| BSD \| HPUX \| LPRNG \| PLP \| QNX \| SOFTQ \| SYSV | 指定要使用的打印系统类型。最常见的打印系统是 BSD。 |
| log file | 路径名 | 指定将 Samba 消息记录到的路径。这通常在 /var/log 目录中。 |
| max log size | 数字 | 指定日志文件允许的最大大小。 |

### 表 8.10 SAMBA [global] 部分变量

