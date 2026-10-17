
# 计划

Linux 上的例行维护任务（如备份）由 `cron` 服务管理，并由 `cron` 守护进程（daemon）实现。守护进程是一个持续运行的服务器，不断检查需要执行的操作。这些任务列在 `crontab` 文件中。`cron` 守护进程会不断检查用户的 `crontab` 文件，以查看何时该执行这些操作。任何用户都可以设置自己的 `crontab` 文件。`root` 用户可以设置 `crontab` 文件来执行系统管理操作，例如在每周或每月的特定时间备份文件。

创建 `cron` 条目可能是一项复杂的任务，这需要使用 `crontab` 命令来修改 `/etc/crontab` 目录下的 `cron` 文件。相反，你可以使用 GUI `cron` 调度工具来轻松设置 `cron` 动作。其中最有用的工具之一是 `Schedule`，它为创建计划命令提供了一个易于使用的界面。使用 `Edit`（编辑）菜单中的 `New`（新建）条目来调度命令，指定时间和日期，以及是否每周或每月重复。模板功能允许你使用之前计划的信息来设置新计划，使用相同或类似的命令但不同的时间。

# 系统日志

在系统上执行任务的各种系统日志存储在 `/var/log` 目录中。在这里你可以找到邮件、新闻以及所有其他系统操作日志（例如 Web 服务器日志）。`/var/log/messages` 文件是未被其他日志涵盖的所有系统任务的日志（见图 12-3）。这通常包括启动任务，例如加载驱动程序和挂载文件系统。

![](img/9a8872dc6f2acaed163529fd9d421e05_389_0.png)

图 12-3：GNOME 系统日志查看器

如果卡的驱动程序在启动时加载失败，你可以在这里找到错误消息。此文件中还会记录登录情况，显示谁尝试登录哪个账户。`/var/log/maillog` 文件记录邮件消息传输和新闻传输。

要查看这些日志，你可以使用 GNOME 日志查看器：应用程序 | 系统工具 | 系统日志。侧边栏列出了不同的日志。选择其中一个将在右侧面板显示该日志。

# 磁盘使用分析器

磁盘使用分析器让你看到所有挂载硬盘分区上的已和可用磁盘空间（图 12-4）。它还会检查 LVM 和 RAID 阵列。使用情况以简单的图表显示，让你看到总共有可用空间及其位置。当你扫描文件系统（点击工具栏上的 `Filesystem` 按钮）时，所有目录的磁盘使用情况将被分析并显示在左窗格和右窗格的图表中。将鼠标悬停在图表的区域上将显示其目录名称和磁盘使用情况。在左侧列表中，每个文件首先显示其使用情况的图表，以及其大小、顶层目录和文件的数量。会显示目录的大小及其内容（文件和目录）。

![](img/9a8872dc6f2acaed163529fd9d421e05_390_0.png)

图 12-4：磁盘使用分析器，应用程序 | 系统工具 | 磁盘使用分析器

# 硬件传感器

许多用户关注的另一个问题是计算机组件的温度和使用情况。GNOME 硬件监控显示你的 CPU、系统、硬盘以及（如果可用）显卡的检测温度，以及你的计算机可能支持的任何其他传感器，例如

## 表 12-2：传感器应用

| 传感器 | 描述 |
| :--- | :--- |
| `lmsensors` | 检测计算机（主板） |
| `hddtemp` | 检测硬盘 |
| `powernow` | 检测 CPU 使用率 |
| `GNOME sensors-applet` | 检测 CPU 频率 |
| `ksensors` | 检测温度 |

## CPU 频率缩放

另一个应用是 CPU 频率缩放，它将显示 CPU 使用率（见图 12-7）。该应用使用 `powernow` 来检测 CPU 的使用情况。大多数现代 CPU 都支持频率缩放，当其任务较少时会降低 CPU 频率。Intel CPU 会降至 60%，AMD 会降至 50%。

图 12-7：CPU 频率缩放

# SELinux：通过 system-config-selinux 进行配置

通过 `system-config-selinux`，你可以管理和配置你的 SELinux 策略，但无法创建新策略。你可以从系统 | 管理菜单访问 `system-config-selinux`。`system-config-selinux` 窗口列出多个面板，侧边栏包含状态、布尔值、文件标记、用户映射、SE 用户、转换、网络端口和策略模块（见图 12-8）。`system-config-selinux` 会调用如 `lestatus` 和 `semanage` 等 SELinux 管理工具并带有相应的选项来执行配置更改。

用户映射显示用户登录名称到 SELinux 用户的映射。最初会有两个映射：`root` 用户和默认用户。

布尔值面板列出了针对目标服务（如 Web 和 FTP 服务器、NFS 和 Samba）的各种选项。通过这些选项，你可以进一步修改每个服务的控制方式。不同服务（如 FTP、Apache Web 服务器和 Samba）有可展开的菜单。例如，FTP 条目让你选择是否允许访问主目录或 NFS 传输。

图 12-8：`system-config-selinux`，应用程序 | 系统工具 | SELinux 管理

## 第 12 章：系统工具

文件标签（File Labeling）面板将列出你的系统目录和文件，显示它们的安全上下文和类型。你可以通过选择项目并点击“属性”（Properties）来编辑文件的属性。这将显示一个包含文件名、类型、SELinux 类型和 MLS 级的对话框。你可以更改 SELinux 类型或 MLS 级别。对于许可（permissive）策略，MLS 级别将为 `s0`，允许任何人访问。你还可以添加或删除条目。

SELinux 用户（SELinux Users）面板显示不同种类的 SELinux 用户。最初，会有几种用户类型，包括 `system_u` 和 `user_u`（见图 12-9）。`root` 用户是 `root` 用户，它对整个系统拥有完全且总额的管理权限。`system_u` 允许用户在需要时管理权限。`user_u` 用于普通用户。每个条目都列出了其 SELinux 用户、SELinux 前缀、MLS 级别、MLS 范围和 SELinux 角色。MLS 级别是访问级别（例如在许可策略下），而 MLS 范围是从 `SystemLow` 到 `SystemHigh` 的访问。给定用户具有某些可用的角色。`root` 用户拥有 `system_r`、`sysadm_r` 和 `staff_r` 角色，允许它拥有系统能力和用户用户访问。`user_u` 也拥有 `system_r` 角色，如果该用户拥有 `root` 密码，则允许用户执行系统管理。

![](img/9a8872dc6f2acaed163529fd9d421e05_394_0.png)

图 12-9：`system-config-selinux` Boolean面板

翻译（Translation）面板允许设置 MLS 符号。最初你会有 `SystemHigh` 以及 `SystemLow–SystemHigh` 范围的符号。通过更改映射的 MLS 级别，来改变整个系统的安全级别。

网络端口（Network Port）面板列出了系统的网络协议、SELinux 类型和 MLS 安全级别。选择一个项目并点击“属性”来更改端口的 SELinux 类型或 MLS 级别。组（Group）视图将显示 SELinux 类型以及其适用的端口列表。此视图不显示 MLS 级别，因为它们是单独应用于端口的。

策略（Policy）面板列出 SELinux 策略模块。在这里，你会看到针对 Thunderbird 和 Evolution 等不同应用程序的模块，以及 USB 和 HAL 等服务设备。列出的还有 GNOME 等桌面。该面板允许你添加或删除模块。你还可以为模块启用或添加审计规则以便日志。

![](img/9a8872dc6f2acaed163529fd9d421e05_395_0.png)

SELinux 拒绝模块使用可能标记错误的文件（`/home/rocket/session-errors`）。这意味着 SELinux 不允许模块使用用户在主目录或 tmp 目录中编辑这些文件，然后移动（`mv`）到系统目录。问题在于文件最终具有了错误的上下文，导致连接的应用程序无法访问。

### 允许访问
如果你想访问这些文件，需要使用 `restorecon -v /home/rocket/session-errors` 对它们进行重新标记。你可能想使用 `restorecon -R /home/rocket/` 对整个目录进行重新标记。

### 附加信息
- 源上下文 (Source Context): `unconfined_unconfined_remanage_t:s0:s0:c10223`
- 目标上下文 (Target Context): `system_u:object_r_home_t0`
- 目标对象 (Target Objects): `/home/rocket/session-errors` [ ]
- 源 (Source): `semodule`
- 源路径 (Source Path): `/usr/sbin/semodule`
- 主机 (Host): `<Unknown>`
- 源 RPM (Source RPM): `richard5`
- 软件包 (Packages): `policycoreutils-2.0.46-5.fc9`
- 审计监听器 (Audit Listener): `8/8`

图 12-10：SELinux 故障排除器，应用程序 | 系统工具 | 故障排除

## SELinux 故障排除

Fedora 包含了 SELinux 故障排除器用于通知 SELinux 检测到的问题。当 SELinux 拒绝访问文件或应用程序时，内核会发出 AVC 通知。这些会被 SELinux 故障排除器分析，以检测用户可能需要处理的问题。当检测到问题时，SELinux 故障排除器通知将在桌面通知区域显示并带有故障排除器图标。点击图标或通知将打开故障排除器。

# 网络分析工具

你可以使用多种网络工具来执行任务，例如获取网络上其他系统的信息、访问其他系统以及与其他用户进行通信。可以使用 `ping`、`finger`、`traceroute` 和 `host` 等工具获取网络信息。像用于 VoIP 的 Ekiga 和 CIQ 等聊天和消息客户端允许你与网络上的其他用户通信。

| 网络信息工具 | 描述 |
|---|---|
| `ping` | 检测系统是否连接到网络。 |
| `finger` | 获取网络上用户的信息。 |
| `who` | 检查当前哪些用户在线。 |
| `whois` | 获取域名信息。 |
| `host` | 获取远程主机的网络地址信息。 |
| `traceroute` | 跟踪消息经过的计算机网络和主机的序列。 |
| `ethereal` | 用于检查网络流量的协议分析器。 |
| `gnome-nettool` | 用于各种网络工具（包括 `ping`、`finger` 和 `traceroute`）的 GNOME 界面。 |
| `mtr` and `xmtr` | My traceroute 结合了 `ping` 和 `traceroute` 操作（系统菜单中的 Traceroute）。 |

表 12-3：网络工具 `gnome-nettool`

# GNOME 网络工具：gnome-nettool

对于 GNOME 桌面，`gnome-nettool` 工具提供了用于输入 `ping` 和 `traceroute` 命令的 GNOME 界面（见图 12-8），以及用于查询网络用户和主机 `Finger`、`Whois` 和 `Lookup`（应用程序 | 系统工具 | 网络工具）。`Whois` 将提供特定域名的域名信息，`Lookup` 将同时提供域名和 IP 地址（见图 12-11）。它还包含了 `netstat` 和 `portscan` 等网络状态工具。第一个面板“设备”（Devices）描述了你连接的网络设备，包括每个设备的配置和传输信息，例如硬件和传输的字节数。IPv4 和 IPv6 主机 IP 地址都会列出。

![](img/9a8872dc6f2acaed163529fd9d421e05_399_0.png)

图 12-11：Gnome 网络工具

# 网络信息：ping, finger, traceroute, and host

你可以使用 `ping`、`finger`、`traceroute` 和 `host` 命令查找网络上系统和用户的状态信息。`ping` 命令用于检查远程系统是否正在运行。你使用 `finger` 来查找网络上其他用户的信息，查看他们是否登录或是否收到了邮件；`host` 显示网络上系统的地址信息，为你提供系统的 IP 和域名地址；而 `traceroute` 可用于跟踪消息传递给你时经过的计算机网络和系统序列。表 12-3 列出了各种网络信息工具。

# ping

`ping` 命令检测系统是否正在运行。`ping` 的参数是你想要检查的系统名称。如果你要检查的系统已关机，`ping` 会发出超时消息，指示无法建立连接。下一个示例检查 `www.redhat.com` 是否运行并连接到网络：

```
ping www.redhat.com
```
