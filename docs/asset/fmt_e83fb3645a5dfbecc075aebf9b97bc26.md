
你不需要每次启动或停止 PPP 都以 root 身份登录，可以为此任务创建登录：一个名为 `pppup` 用于启动 PPP，另一个名为 `pppdown` 用于停止它。通过将这些登录项的用户 ID 设置为 0，它们将以 root 身份运行。将它们的 shell 设置为你想要运行的脚本名称。

## 域名服务器

你可以在 `/etc/resolv.conf` 中列出最多三个名称服务器，且必须按 IP 地址列出。它们按照在文件中出现的先后顺序进行搜索。下面的代码段描述了我的 `/etc/resolv.conf` 文件。`search` 行设置默认域名为 `fylz.com`。此行指示网络应用程序在尝试 DNS 查找之前，在任何收到的没有域名的地址后附加 `fylz.com`。例如，如果我使用邮件地址 `visi@smiley` 作为邮件目标，执行 DNS 查找的程序会在执行查找之前向该地址附加 `fylz.com`。

```
fylz.com
nameserver 204.157.220.4
nameserver 204.157.223.111
```

## 新闻服务器

新闻阅读器是允许读取 Usenet 新闻组的程序，这是一个包含超过 20,000 个不同在线讨论组的集合。大多数新闻阅读器使用 `NNTPSERVER` 环境变量的值来寻找新闻服务器。要检查该变量是否设置正确，请在 shell 提示符输入 `echo $NNTPSERVER`。

## 电话号码和登录序列

大多数系统将文件放在 `/etc/ppp` 目录下。Red Hat 发行版将文件放在 `/etc/sysconfig/network-scripts` 中，以便其图形化网络设置程序访问的所有文件都在同一个目录下。`chat` 程序需要一个文件来作为如何建立连接的指令。该文件可以放在任何地方，只要它是安全的且 `chat` 程序知道在哪里找到它即可。该文件包含一些 `chat` 关键字指令，以及让调制解调器通话、拨打号码和执行登录的序列。请参见本部分前面的“The chat program”以获取此文件的示例。

如果其他人看到了你的电话号码和登录序列，你就失去了对 ISP 账户的独占控制权。确保这些文件的权限不允许 root 以外的任何用户访问。

## pppd 程序

`pppd` 程序在建立连接后处理拨号连接。

```
pppd [tty] [speed] [options]
```

| 选项或参数 | 功能 |
| :--- | :--- |
| tty | 与调制解调器通信的设备。如果你不指定设备，`pppd` 将使用控制终端（你输入 `pppd` 命令的设备）。除非你非常擅长输入 PPP 数据包，否则你通常不想让 `pppd` 使用控制终端。如果你指定了一个没有以 `/dev` 开头的设备，`pppd` 会为其加上。 |
| speed | 链接中使用的波特率。 |
| options | 一组定义链接操作特性的选项。这些是 `/etc/ppp/options` 和 `$HOME/.pprc` 中指定选项的额外选项。你可以通过在关键字前加 `-`（例如 `-crcts`）来关闭布尔选项（如 `crcts`）。如果某个选项的默认值是关闭，则使用 `+option` 将其开启。 |

以下列表包含了额外的 `pppd` 选项。请查看 `pppd` 的 man 页面（man 的第 8 节）获取更完整的列表。

## 使用 PPP 网络

| 选项 | 功能 |
| --- | --- |
| asyncmap map | 使用 map 建立哪些控制字符无法通过串行线路接收。这是一个以八进制指定的 32 位位图，其中每个位代表一个控制字符。位 0 (00000000) 代表字符 0x00；位 31 (10000000) 代表字符 0x1F。 |
| auth connect cmd | 要求对端进行身份验证。使用指定的程序或 shell 命令建立串行连接。`chat` 的调用将在此处。 |
| crtscts default | 使用硬件 (RTS/CTS) 流控制。 |
| defaultroute | 为此连接向系统路由表添加默认路由。 |
| disconnect cmd | 运行 `pppd` 以终止链接。 |
| escape xx,yy | 转义指定的字符。 |
| file optf | 从指定文件读取选项。 |
| mru n | 设置最大接收单元。 |
| mtu n | 设置最大传输单元。 |
| netmask n | 指定此接口的掩码。 |
| silent | 在远程系统发送有效包之前不发送任何内容。 |
| local:remote | 设置本地和/或远程地址。 |
| bsdcomp nr,nt | 请求远程系统压缩包使用 BSD 压缩。nr 指定最大尺寸。如果你未指定 nt，则 nt 默认为 nr。 |
| -bsdcomp | 关闭 BSD 压缩。 |

## 使用 PPP 网络 (续)

| 选项 | 功能 |
| --- | --- |
| +chap | 要求 CHAP（密码握手协议）身份验证。 |
| -chap | 不需要 CHAP。 |
| debug | 增加当前调试级别。 |
| detach | 分叉到后台进程。 |
| dns-addr ip | 设置 DNS 服务器的 IP 地址。配合 Microsoft 客户端。 |
| domain d | 为验证目的向主机附加域名 d。 |
| -ip | 禁用 IP 协商。 |
| ipparam string | 将此字符串作为第六个参数发送给 `ip-up` 和 `ip-down` 脚本。 |
| kdebug n | 在内核级 PPP 驱动中启用调试代码。这是一个八进制数字，通过加1（通用调试消息）、2（接收包内容）和4（发送包内容）形成。 |
| login | 使用系统密码数据库对对端 PAP 进行身份验证。 |
| modem | 使用调制解调器控制线（默认）。 |
| name nam | 为验证目的将本地系统名称设置为 *nam*。 |
| +pap | 要求 PAP 身份验证。 |
| papcrypt | 指定密钥已加密。在本地系统的 ARP 表中添加远程系统的 IP 地址和本系统的以太网 MAC 地址。 |
| remotename nam | 假设远程系统名称为 *nam* 用于身份验证。 |
| +ua file | 如果远程请求则使用 PAP 进行身份验证，并使用指定 *file* 的内容作为用户名和密码。 |
| usehostname | 强制使用主机名作为本地系统名称。不允许使用 name 选项。 |
| user u | 将用户名设置为 *u* 用于 PAP 身份验证。 |
| xonxoff | 使用软件流控制。除非无法使用硬件流控制，否则不要使用此选项，因为它会增加开销且往往不可靠。 |

## 为用户登录设置串口

`pppd` 程序会在以下位置查找前三页中列出的选项：

- `/etc/ppp/options`
- 你的家目录下的 `.pprc`
- 命令行

认证密钥保存在以下位置：

- `/etc/ppp/pap-secrets` 用于 PAP
- `/etc/ppp/chap-secrets` 用于 CHAP

以下程序是我用于 ISP（互联网服务提供商）时使用的脚本：

```
/usr/sbin/pppd asyncmap 0000000 crtsuts \
modem lock defaultroute \
netmask 255.255.255.0 /dev/tty 57600 \
connect "/usr/sbin/chat -v -f /etc/ppp/ppp-aa"
```

我还在 `/etc/ppp/ip-up` 文件中添加了以下两行，它们会在 PPP 连接建立后自动执行。这会将我的 PPP 链路上的最大数据包大小设置为 2966（慢速链路的良好选择），然后执行一个命令，将我的计算机时钟与一个已知准确的时钟进行同步。该文件也是启动 `fetchmail` 以自动下载你电子邮件的良好位置。

```
/sbin/ifconfig ppp0 mtu 2966
/bin/bind/rate www.isc.com
```

## 为用户登录设置串口 (续)

当 LINUX 系统启动时，`init` 使用 `/etc/inittab` 中的信息在控制台上启动程序，并且串口允许用户登录。启动的程序之一是 `getty`（或 `mgetty`，一个带有额外选项的变体，例如处理 FAX 连接的能力）。`getty` 执行以下操作：

- 打开线路并设置其模式，例如行传输速率。
- 等待登录指示，获取用户名，并将控制权移给 `login` 程序。

两个版本的 `getty` 使用不同的配置文件：

- `getty` 使用名为 `/etc/default/getty.line` 的文件来配置每条单独的线路。
- `mgetty` 使用 `/etc/mgetty+sendfax` 目录下的文件，其中 `mgetty.config` 是主配置文件。

## 关闭 LINUX

作为系统管理工作的一部分，你可能被要求以有序且安全的方式关闭 LINUX。要做到这一点，你必须遵循以下步骤：

1. 通知所有已登录的用户系统即将关闭。
2. 阻止新登录。
3. 通知所有程序系统即将关闭（以便它们可以进行清理工作）。

```
shutdown [-h] [-r] time [message]
```

| 选项或参数 | 功能 |
|---|---|
| -h | 关机后停止系统 |
| -r | 关机后重启系统（默认）。 |
| time | 执行关闭的时间。可以是指定为 hh:mm 的绝对时间，也可以是在执行关闭前等待的分钟数，指定为 +mins。命令 `now` 是 +mins 的同义词。 |
| message | 发送给所有用户的消息。 |

若要在 5 分钟后关闭系统并通知用户系统将关闭 30 分钟，你需要输入 `shutdown -h +5 "Back up in 30 minutes"`。

每个用户都会收到一条类似这样的消息：

> Broadcast message from root (tty3) Wed Oct 8 15:16:17 1997 ... Back up in 30 minutes. The system is going DOWN for system halt in 5 minutes !!

不要简单地按下重置键或关闭电源来关闭系统。LINUX 缓存了大量信息（为了高效运行）。如果你不给 LINUX 留出清理的机会，你的文件可能会损坏。Linux 文件系统非常擅长从这种掉电中恢复，但这不能作为冒险损坏系统风险的借口。

## 启动 LINUX

你在安装 LINUX 时配置 LILO（引导加载程序）的方式决定了系统的启动方式。你可能以三种模式之一安装了 LILO：

- 立即启动 LINUX。
- 等待预定的时间（例如五秒）然后启动某个操作系统。
- 等待在 LILO 提示符处输入系统 ID 为止。

有关配置 LILO 的更多信息，请参阅《LINUX SECRETS, 2nd Edition》中的“Installing LILO”（安装 LILO）章节。无论你如何配置 LILO，以下步骤都适用：

1. 当计算机启动时，按住 Shift 键并等待 LILO 提示符。
2. 释放 Shift 键并按 Tab 键。LILO 会显示启动选择列表（例如 DOS、LINUX，或你在配置 LILO 时决定输入的任何内容）。
3. 输入你的选择并按 Enter。LILO 会找到并加载你选择的系统。

如果你刚刚启动了 LINUX 并想回去检查启动消息，可以使用 `Shift+PageUp` 和 `Shift+PageDown` 翻页查看。

## 使用 cron 程序

`cron` 程序在启动时启动并每分钟运行一次。`cron` 随后运行任何计划在当前运行的任务。调度的任务位于 `/etc/crontab`（系统 crontab 文件）或 `/var/spool/cron/crontabs` 目录中以单个用户名命名的文件中。

要更改系统 crontab 文件...

## 运行级别

运行级别允许系统处于不同的状态。每个级别代表一组活动状态的服务。例如，你可以根据需要在不同级别之间切换。

### 切换运行级别

你使用 `/sbin/init` 来更改运行级别。要切换到新级别，请遵循以下步骤：

1. 以 root 身份登录。
2. 输入 `telinit` 后接所需的级别（0 到 6）。

如果你编辑了 `/etc/inittab` 并想切换到单用户模式，请输入 `telinit s`。

| 运行级别 | 用途 |
|---|---|
| 0 | 系统关机 |
| 1 | 单用户模式 (Red Hat) |
| 2 | 无网络的多用户模式 (Red Hat) |
| 3 | 完全多用户模式 (Red Hat) |
| 4 | 仅运行 X 多用户 (Slack) |
| 5 | 多用户 (Slack); 带 X 的多用户 (Red Hat) |
| 6 | 重启 |

### 电源故障/恢复时的操作

```
pf::powerwait:/etc/init.d/powerfail start
np::powerfailnow:/etc/init.d/powerfail now
p::powerokwait:/etc/init.d/powerfail stop
```

### 用于运行级别的 /sbin/getty 调用

```
# "id" 字段必须与设备名称的最后
# 字符相同（"tty" 之后）。
# 格式：
# <id>:<run levels>:<action>:<process>

1:2345:respawn:/sbin/getty 38400 tty1
2:23:respawn:/sbin/getty 38400 tty2
3:23:respawn:/sbin/getty 38400 tty3
4:23:respawn:/sbin/getty 38400 tty4
5:23:respawn:/sbin/getty 38400 tty5
6:23:respawn:/sbin/getty 38400 tty6

# 在串口线上放置 getty 的示例
#（用于终端）
#
T1:23:respawn:/sbin/getty -L ttyS1 19200 vt100

# 在调制解调器线路上放置 getty 的示例。
#
T3:23:respawn:/sbin/mgetty -x0 -s 57600 ttyS3
```

### 在运行级别目录中设置文件

`init` 程序处理运行级别的变化。当发生这种变化时，`init` 将执行以下操作：

- 执行旧运行级别目录中所有以字母 `K` 开头的脚本；`init` 按照 `ls` 命令输出的显示顺序执行脚本。
- 执行新运行级别目录中所有以字母 `S` 开头的脚本；`init` 按照 `ls` 命令输出的显示顺序执行脚本。

例如，假设你正处于运行级别 2，并将运行到级别 3。同样假设 `rc2.d` 目录中的文件为 `K10_umount`、`S10_doit` 和 `S20_startgoodstuff`，而 `rc3.d` 目录中的文件为 `K10_nfs`、`K20_rpc`、`K30_zap`、`S10_nfs`、`S20_rpc` 和 `S40_greet`。`init` 将执行 `rc2.d/K10_umount`、`rc3.d/S10_nfs`、`rc3.d/S20_rpc`，最后执行 `rc3.d/S40_greet`。

## 系统运行级别

当你启动 LINUX 时，需要启动各种程序。为了使程序选择可配置，存在一个 `/etc/inittab` 文件以及一组包含启动脚本或程序的目录。在 Red Hat 上，这些目录位于 `/etc/rc.d` 目录中。在 Debian 上，它们位于 `/etc`。虽然不同的 Linux 发行版之间存在某些差异，但下表提供了概览：

| 文件名 | 功能 |
|------|---|
| init.d | 所有启动文件的主目录。每个运行级别都链接回此目录中的文件。 |
| rc | 初始启动文件。当运行级别改变时也会执行它。在 Debian 上，一个名为 `rc.boot` 的目录包含启动文件。 |
| rc0.d | 在运行级别 0 下运行的文件目录。 |
| rc1.d | 在运行级别 1 下运行的文件目录。 |
| rc2.d | 在运行级别 2 下运行的文件目录。 |
| rc3.d | 在运行级别 3 下运行的文件目录。 |
| rc4.d | 在运行级别 4 下运行的文件目录。 |
| rc5.d | 在运行级别 5 下运行的文件目录。 |
| rc6.d | 在运行级别 6 下运行的文件目录。 |
| rc.local | 本地配置文件。 |
| rc.sysinit | 启动时运行的文件。（仅限 Red Hat。） |

上述描述的运行级别方案源自 UNIX System V。一些早期的 LINUX 发行版并不使用它。它们使用基于 Berkeley Unix 的系统，每个运行级别使用文件而不是目录。这些文件的名称如 `rc.1`、`rc.2` 等。基本概念是相同的，但你必须编辑多个文件才能影响多个运行级别的更改。

除了运行级别和目录外，`/etc/inittab` 控制系统在每个运行级别下的操作。该文件中的每一行都是由冒号分隔的命令序列，其格式如下：

```
id:runlevels:action:process
```

字段定义如下表所示：

| 字段 | 功能 |
|---|---|
| id | 一个一到四个字符的标识符，唯一标识该行。 |
| runlevels | 数字字符串，用于标识激活此条目的运行级别。例如，字符串 `235` 表示此条目将在运行级别 2、3 和 5 下激活。 |
| action | 针对此条目采取的操作（见下表）。 |
| process | 要执行的进程。 |

下表列出了 `action` 的有效选择：

| 关键字 | 含义 |
| --- | --- |
| boot | 在系统引导时执行进程。 |
| bootwait | 在系统引导时执行进程，并等待其结束。 |
| initdefault | 指定默认运行级别。 |
| powerfail | 电源故障时执行。 |
| powerokwait | 电源恢复时执行。 |
| powerwait | 电源故障时执行，并等待其结束。 |
| respawn | 进程终止时重新启动。 |
| sysinit | 系统初始化时执行。 |
| wait | 切换到特定运行级别时执行，并等待其结束。 |
| once | 切换到特定运行级别时执行一次。 |
| off | 什么都不做。 |
| ondemand | 按需执行。 |
