
10. 你可以运行哪两个命令来激活对 `/etc/samba/smb.conf` 文件的更改？

a. `smclient --restart`

b. `rcsnmb restart`

c. `nmbclient --restart`

d. `rcsnmb restart`

11. 你可以使用什么命令检查 `/etc/samba/smb.conf` 文件是否存在错误？

12. 使用什么命令可以使用 SMB 将服务器 `arfa` 上的 `acctg` 共享目录挂载到本地的 `/mnt` 目录？

13. 哪些守护进程运行在 NIS 服务器上？（选择所有适用项）。

a. `ypbind`

b. `ypwwhich`

c. `ypserv`

d. RPC portmapper

14. 使用什么命令可以根据 `/var/yp/Makefile` 中的条目在命令行生成 NIS 映射？

15. 你已经配置了系统向 NIS 服务器进行身份验证。当你使用 `password` 命令更改密码时，它没有按预期变化。你必须使用什么命令更改 NIS 密码，使其在 NIS 服务器上生效？

16. 下列哪项是 LDAP 对象的有效 DN？

a. `cn=joe`

b. `cn=joe.ou=acctg`

c. `cn=joe.ou=acctg.dc=suse`

d. `cn=joe.ou=acctg.dc=suse.dc=com`

17. SLES 9 中使用哪个包来实现 LDAP？

## 探索性练习

### 配置 Samba 域控制器

使用互联网研究将你的 Samba 服务器用 Windows 域控制器所需的步骤。接下来，以 root 用户身份登录 `tty1`，通过编辑 `/etc/samba/smb.conf` 文件将你的 Samba 服务配置为域控制器。该文件中至少需要的行如下：

```
[global]
domain logons = yes
security = user
encrypt passwords = yes
wins support = yes
netbios name = ________________（在此处输入你的域名）
```

```
[netlog]
path=/netlog（使用权限 777 创建此目录）
public = no
writable = no
locking = no
```

接下来，在系统中创建一个新用户（`useradd -m testuser`），并为 samba 数据库中的该用户提供一个加密密码（`smbpasswd testuser`）。然后，通过向 `/etc/passwd` 和 `/etc/shadow` 添加行，为每个将加入你 Linux 计算机域的 Windows XP 客户端添加计算机账户，并在计算机名后加上一个 $ 字符：

```
/etc/passwd 示例行：
clientcomputename$:x:5000:5000::/dev/null:/bin/false
```

```
/etc/shadow 示例行：
clientcomputename$:*:6445::::
```

完成后，通过将 Windows 客户端加入域并测试域登录来测试你的配置。完成后，退出 Samba 服务器上的 `tty1`。

### 研究文件和打印机共享协议

使用互联网寻找三个使用 SLES 的组织。总结每个公司网络基础设施和配置中使用的文件和共享协议。对于每个组织，提供使用每项技术的理由。

### 配置 LDAP

作为 root 用户，使用 YaST 配置你的系统。完成后，通过将 Windows 客户端加入域并测试域登录来测试你的配置。完成后，退出 Samba 服务器上的 `tty1`。

### 第 9 节

在本节中，你将学习启用某些 Internet 服务的基础知识

- 配置 SUSE Linux 服务器

- 启用 Internet

- 启用 Apache

- 启用 FTP

选择 GMT 作为硬件时间可以更容易协调位于不同地的大量计算机（特别是当这些计算机位于不同时区时）。

## 时间配置文件

当前时间（系统时间）是通过 `/etc/sysconfig/clock` 文件中的 `TIMEZONE` 变量来计算的，该变量还处理了夏令时和标准时间之间的必要更改。

以下是 `/etc/sysconfig/clock` 设置的示例：

```
HWCLOCK="--localtime"
TIMEZONE="Europe/Berlin"
DEFAULT_TIMEZONE="Europe/Berlin"
```

通过 `TIMEZONE` 变量，本地主机（=系统时间）配置的时间会被设置 `/usr/share/zoneinfo/localtime` 文件（指向 `/etc/localtime` 的符号链接）。

`/usr/share/zoneinfo/` 目录是所有时区的数据库。

你可以通过输入以下命令查看硬件钟：

```
cat /proc/driver/rtc.
```

## 如何使用 hwclock 和 netdate 同步时间

要使用 `hwclock` 和 `netdate` 同步网络服务器之间的时间，你需要了解以下：

- 如何使用 hwclock

- 如何使用 netdate

## 如何使用 hwclock

`hwclock` 是一个访问硬件钟的工具。你可以显示当前时间、将硬件钟设置为指定时间、将硬件钟设置为系统时间，以及从硬件钟设置系统时间。

你可以定期运行 `hwclock` 来向硬件钟中添加或移除时间，以补偿系统漂移（如果让它运行，会以一定的速率持续增加或减少时间）。

`hwclock` 使用多种方法来获取和设置硬件钟值。正常方法是初始化一个 I/O 进程指向设备设备 `/dev/share/rtc`，它由 `rtc` 驱动维护。

然而，这种方法并不总是可用。`rtc` 驱动是 Linux 较晚添加的，在旧版系统中不可用。

## 配置 SUSE Linux Enterprise Server 553

在旧版系统中，访问硬件钟的方法取决于系统硬件。

> 注意：关于系统如何访问硬件钟以及其他 `hwclock` 选项的更多细节，请参见 `hwclock` 的 man 页面 (`man hwclock`)。

表 9-1 列出了一些常用的 `hwclock` 选项。

表 9-1

| 选项 | 描述 |
| :--- | :--- |
| `-r` or `--show` | 此选项显示硬件钟的当前时间。即使你将硬件钟设置为 UTC 时间，时间也始终显示为本地时间。 |
| `-w` or `--systohc` | 此选项将硬件钟设置为当前系统时间。 |
| `-s` or `--hctosys` | 此选项将系统时间设置为当前硬件钟时间。它还会将内核的时区值设置为由 `TZ` 变量指示的本地时区。 |
| `-a` or `--adjust` | 此选项向硬件钟增加或减去时间以补偿系统漂移（详情请输入 `man hwclock`）。 |
| `-v` or `--version` | 此选项显示 `hwclock` 的版本。 |
| `--set--date=newdate` | 此选项将硬件钟设置为 `--date` 选项指定的日期。例如：`hwclock --set--date="9/22/07 16:45:05"` |

## 如何使用 netdate

若仅设置一次系统时间，可以使用如下方式使用 `netdate` 命令：`netdate timeserver1 timeserver2...`

其中 `timeserver` 代表网络或互联网上的时间服务器。

在查询时间服务器后，`netdate` 客户端会将它们的时间与自己的时间进行比较。时间差然后会被分组，以确定哪一组是最大的服务器（在一定范围内）。组中的第一台计算机用于更新本地服务器的时间。

要将时间同步到特定的外部时间源，你输入如下内容的 `netdate time_source`：

```
netdate ptbtime1.ptb
```

## 第 9 节启用互联网服务

在这种情况下，客户端查询位于德国布伦斯维克的德国物理技术联邦 (PTB) 的时间服务器。

然后你需要通过输入 `hwclock --systohc` 或 `hwclock -w` 将硬件钟设置为系统钟时间。

> 注意：使用 `netdate` 和 `hwclock` 实现时间同步的最简单方法是使用由 `cron` 定期运行的脚本。

## 什么是网络时间协议 (NTP)

随着网络环境不断扩展到混合操作系统环境，时间同步变得越来越依赖 NTP。

要在 SUSE Linux Enterprise Server 上配置 NTP，你需要理解以下内容：

- NTP

- 层级 (Stratum)

- NTP 守护进程 (`xntpd`)

- NTP 术语

- NTP 守护进程的工作原理

> 注意：本节旨在教你一些 NTP 的基本概念。更多关于 NTP 的信息，请访问 www.ntp.org。

## NTP

NTP 是一种行业标准协议，使用端口 123 UDP 在时间提供者和时间消费者之间进行通信。
