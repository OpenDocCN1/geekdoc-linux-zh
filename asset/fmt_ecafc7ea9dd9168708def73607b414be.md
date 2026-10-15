
```
Fedora Core release 3 (Heidelberg)
Kernel 2.6.10-1.770_PC3 on i686
```

## issue.net

此文件包含与 `/etc/issue` 相同的内容。当你尝试 `telnet` 登录系统时，它会显示。由于通过互联网连接到你系统的人可以看到，你应该更改此消息以包含警告信息，例如“访问正在被监控。禁止未经授权的访问”。

## /etc/aliases

`/etc/aliases` 是 `Sendmail` 程序的电子邮件别名文件，`Postfix` 使用 `/etc/postfix/aliases`。默认情况下，它包含许多系统账户别名。别名文件会将所有基本系统账户（如 `bin`、`daemon` 和 `operator`）的邮件发送到 `root` 的邮箱箱。

其他常见的电子邮件别名，例如，将所有 `root` 的邮件发送给通常以 `root` 身份运行的用户。所以如果 `taleen` 大多数时间都以 `root` 身份运行，她可以将 `root` 的邮箱箱别名为她自己的邮箱箱。这样，她就不需要登录 `root` 就能阅读重要的系统邮件了。

在启动时运行 `fsck` 时，它还会检查 `fstab` 中列出的文件系统的一致性。它会修复损坏的文件系统，通常是因为系统崩溃或突然断电时没有正确挂载这些系统。`fs_passno` 值为 `0`（最后一列的数字）的文件系统在启动时不会被检查。如列表 8-2 所示，几乎所有文件系统在启动时都会被检查，软驱除外，`fsck` 在启动时不会检查软驱。

`fstab` 行有六个字段，每个字段代表不同的配置值。第一个字段描述文件系统，它可以是分区名称、磁盘分区的标签、逻辑卷或远程文件系统。第二个字段是用于访问文件系统的挂载点。第三字段描述文件类型。第四个字段用于你可能需要的任何挂载选项。第五个字段是 `0` 或 `1`，决定 `dump` 是否备份此文件。最后一个字段设置了 `fsck` 检查这些系统的顺序。

```
# 此文件由 fstab-sync 编辑 - 详情请 'man fstab-sync'
/dev/VolGroup00/LogVol00  ext3 defaults      1 1
LABEL=/boot               ext3 defaults      1 2
none                      /dev/pts  devpts gid=5,mode=620 0 0
none                      /dev/shm   tmpfs            0 0
none                      /proc       proc             0 0
none                      /sys        sysfs defaults      0 0
/dev/VolGroup00/LogVol01 swap       defaults      0 0
/dev/hdc                 /media/recorder auto 0 0
pconsole,exec,noauto,fscontent=system_u:object_r:removable_t,managed
```

列表 8-2 典型的 `fstab` 文件。

## grub.conf

`GRUB` 是现代缩写 `Grand Unified Bootloader`（大统一引导加载程序）。它是 `Fedora Core` 和 `Red Hat Enterprise Linux` 使用的默认引导程序。它的图形界面让你可以在已安装的操作系统和你想运行的内核之间进行基础选择 `/etc/grub.conf` 文件是位于 `/boot/grub/grub.conf` 的实际文件的符号链接。

列表 8-3 显示了一个典型的 `grub.conf` 文件。

```
## grub.conf 由 anaconda 生成
# 注意，修改此文件后，你不需要重新运行 grub
# 通知：你有一个 /boot 分区。这意味着
    # 所有内核和 initrd 路径都相对于 /boot/，例如
    root (hd0,1)
    kernel /vmlinux-root root=/dev/VolGroup00/LogVol00
    initrd /initrd-version.img
#root=/dev/hda
default=5
splashimage=(hd0,1)/boot/grub/splash.xpmz
hiddenmenu
password --md5 1$ANJI7KLJ$/NO0BfkCtkMMapZxG8WK10
```

列表 8-3 一个典型的 `GRUB` 配置文件。（继续）

```
title Fedora Core (2.6.10-1.770_FC3)
root (hd0,1)
    kernel /vmlinux-2.6.10-1.770_FC3 root=/dev/VolGroup00/LogVol00
    initrd /initrd-2.6.10-1.770_FC3.img
title Fedora Core (2.6.10-1.770_FC3)
root (hd0,1)
    kernel /vmlinux-2.6.10-1.770_FC3 root=/dev/VolGroup00/LogVol00
    initrd /initrd-2.6.10-1.770_FC3.img
title Fedora Core (2.6.10-1.770_FC3)
root (hd0,1)
    kernel /vmlinux-2.6.10-1.770_FC3 root=/dev/VolGroup00/LogVol00
    initrd /initrd-2.6.10-1.770_FC3.img
title Fedora Core (2.6.10-1.770_FC3)
root (hd0,1)
    kernel /vmlinux-2.6.10-1.770_FC3 root=/dev/VolGroup00/LogVol00
    initrd /initrd-2.6.10-1.770_FC3.img
```

## 检查系统配置文件

`syslog` 守护进程记录本地系统上的任何重大事件。它可以将这些日志存储在本地文件中，也可以发送到远程日志主机。当作为远程日志主机时，它还可以接收来自其他机器的日志。这些选项以及日志的详细程度等在 `syslog.conf` 文件中设置。

## cron 文件

`cron` 是一个根据预设调度执行命令的守护进程。它每分钟唤醒一次并检查所有 `cron` 文件以查看需要运行哪些任务。`cron` 文件可以由用户或管理员设置以处理系统任务。

> 注意：不要手动编辑 `/var/spool/cron` 目录下的文件。

用户 `cron` 存储在 `/var/spool/cron/`。它们根据所属的用户命名。系统 `cron` 文件存储在 `/etc` 的以下子目录下：

- `cron.d`
- `cron.daily`
- `cron.hourly`
- `cron.monthly`
- `cron.weekly`

`/etc` 目录下的 `crontab` 类似于主控制文件，设置为每天运行 `cron.daily` 目录中的所有脚本，每小时运行 `cron.hourly` 中的所有脚本，同样的 `cron.monthly` 和 `cron.weekly`。`cron.d` 用于存放与 `/etc cron` 文件调度不同的维护文件。默认情况下，`cron.d` 中的一个名为 `sysstat` 的文件每 10 分钟、24 小时运行一次系统活动统计工具。

## syslog.conf

列表 8-4 摘展示了语法和逻辑，即所有级别为或高于消息都应记录在 `/var/log/messages` 文件中。第一条目还表明，任何认证和 `cron` 消息、私有消息应该记录在其他地方。按类型或程序分离日志文件，可以更方便地搜索日志。该行之后的行指定了这些消息应该记录的其他位置。

身份验证权限消息包含某些敏感信息，因此它们记录在 `/var/log/secure` 中。此文件仅允许 `root` 读取，而 `/var/log/messages` 有时被设置为所有人可读。

## 检查系统配置文件 173

或者至少访问控制较那么松。默认情况下，`/var/log/messages` 也被设置为仅允许 `root` 用户读取。

所有消息都记录在 `/var/log/maillog`，`cron` 消息保存在 `/var/log/cron`。`uucp` 和关键级守护进程日志消息保存到 `/var/log/spooler`。所有这些日志文件默认都设置为仅允许 `root` 用户读取。紧急消息会发送到 `syslog.conf` 文件中包含的所有日志文件中，包括控制台。

```
# 将所有内核消息记录到控制台。
# 记录太多其他内容会导致屏幕频繁刷屏。
#kern.*
	/dev/console
# 记录（邮件外）所有级别为 info 或更高的任何内容。
# 不要记录私有的身份验证消息！
*.info;mail.none;authpriv.none;cron.none
	/var/log/messages
# authpriv 文件有限制访问。
authpriv.*
	/var/log/secure
# 将所有邮件消息记录在一个地方。
mail.*
	/var/log/maillog
```

```
# 记录 cron 内容
cron.*
	/var/log/cron
# 所有人接收紧急消息
*.emerg
	*
# 将级别为 crit及更高的新闻错误保存到特殊文件中。
uucp,news.crit
	/var/log/spooler
# 将启动消息也保存到 boot.log
local7.*
	/var/log/boot.log
```

```
# 记录（邮件外）所有级别为 info 或更高的任何内容。
# 不要记录私有的身份验证消息！
*.info;mail.none;news.none;authpriv.none;cron.none
	/var/log/messages
# authpriv 文件有限制访问。
authpriv.*
	/var/log/secure
# 将所有邮件消息记录在一个地方。
mail.*
	/var/log/maillog
# 记录 cron 内容
cron.*
	/var/log/cron
```

**列表 8-4** `/etc/syslog.conf` 文件的部分节录。（续）

# 第 8 章

```
# 所有人接收紧急消息
*.emerg

# 将级别为 crit及更高的新闻错误保存到特殊文件中。
uucp.news.crit /var/log/spooler
```

列表 8-4（续）

# ld.so.conf

此配置文件由 `ldconfig` 使用，`ldconfig` 用于配置动态链接器的运行时绑定。它包含一个存放共享库的目录列表。共享库文件通常以 `.so` 结尾，而静态库文件通常以 `.a` 结尾，表示它们是对象的归档。

如果你安装了一个带有共享库的程序，但该共享库安装在 `ld.so.conf` 文件未列出的不同库目录，那么你可能需要编辑此文件。在这种情况下，你将在运行时收到库不存在的错误。

在这种情况下可以采取的自己的故障排除步骤是运行可执行文件运行 `ldd`，它会打印共享库依赖项。输出如下：

```
[root@terry]# ldd /bin/bash
libmercap.so2 => /lib/libmercap.so2 (0x40026000)
libdl1.so.2 => /lib/libdl1.so.2 (0x0402a000)
libc.so.6 => /lib/tls/libc.so.6 (0x42000000)
lib/ld-linux.so.2 (0x40000000)
```

你可以在列表 8-5 中看到库目录的默认列表。

```
include ld.so.conf.d/*.conf
/usr/X1R6/lib
/usr/lib/qt-3.3/lib
/usr/lib/mysql
```

列表 8-5 一个典型的 `ld.so.conf` 文件。

# logrotate.conf

`logrotate.conf` 和 `logrotate.d` 目录下的文件决定了 `logrotate` 程序如何轮转你的日志文件。日志轮是指删除旧日志文件并将其替换为更新日志的过程。`logrotate` 可以自动轮转、压缩、删除并发送你的日志文件。日志文件可以根据大小或时间（每日、每周或每月）进行轮转。

从列表 8-6 显示的默认 `logrotate.conf` 文件可以看出，大多数设置如何和何时轮转系统日志的选项都是一目易懂的。

对于每个使用 `syslogd` 进行记录且在 `logrotate.d` 中有单独日志轮转配置文件的程序，`/etc/syslog.conf` 中的所有日志条目都应该有一个 `logrot` 配置文件，以及由 `Apache` 等极端应用程序产生的日志文件。这是因为 `syslog` 需要将这些程序的日志条目保存在单独的文件中，以便日志文件可以相互独立地轮转。

```
# 详情请参 "man logrotate"
# 每周轮转日志文件
weekly

# 保留 4 周的备份
rotate 4

# 在轮转旧文件后创建（空）日志文件
create

# 如果你想压缩日志文件，请取消此注释
#compress

# RPM 包将日志轮转信息存入此目录
include /etc/logrotate.d

# 没有 wtmp 包 -- 我们将在这里轮转它们
/var/log/wtmp
monthly
create 0664 root wtmp
rotate 1

# 系统特定的日志也可以在这里进行配置。
```

**列表 8-6** `logrotate.conf` 文件。

## 检查系统配置文件

- `Multiple_IO=16`：设置为 16 允许每个 I/O 中断处理多个扇区。启用此功能可以减少 30% 到 50% 的操作系统开销。请谨慎使用。
- `EIDE_32BIT=3`：为接口卡启用 `(E)IDE 32-位 I/O` 支持。
- `LOOKAHEAD=1`：启用驱动器读取读预取。
- `EXTRA_PARAMS`：指定可以添加额外参数的位置。

## /etc/sysconfig/hwconf

`/etc/sysconfig/hwconf` 文件列出了 `kudzu` 在您的系统中检测到的所有硬件，以及使用的驱动程序、供应商 ID (`vendor ID`) 和设备 ID (`device ID`)。`kudzu` 程序负责检测并配置系统中新的硬件。`/etc/sysconfig/hwconf` 文件不应手动编辑。如果您对其进行了编辑，设备可能会突然显示为已添加，或者在移除后不再显示。

## /etc/sysconfig/i18n

`/etc/sysconfig/i18n` 文件设置默认语言，例如：

```
LANG="en_US"
```

## /etc/sysconfig/init

`/etc/sysconfig/init` 文件控制系统在启动过程中的显示和功能。可以使用以下值：

- `BOOTP=value`，其中 `value` 为以下值之一：
- `BOOTUP=color`：意味着标准的彩色启动显示，设备和启动的成功或失败将用不同的颜色显示。
- `BOOTUP=verbose`：意味着旧式显示，比纯的成功或失败消息提供更多信息。
- 其他任何内容：意味着新的显示方式，但不包含 ANSI 格式。
- `RES_COL=value`，其中 `value` 是状态标签开始的屏幕列数。默认值为 60。
- `MOVE_TO_COL=value`，其中 `value` 将光标移动到 `RES_COL` 行指定的值处。默认值为 `echo -..` 输出的 ANSI 序列。
- `SETCOLOR_SUCCESS=value`，其中 `value` 设置为表示成功的颜色。默认值为 `echo -e` 输出的 ANSI 序列，将颜色设置为绿色。
- `SETCOLOR_FAILURE=value`，其中 `value` 设置为表示失败的颜色。默认值为 `echo -e` 输出的 ANSI 序列，将颜色设置为红色。
- `SETCOLOR_WARNING=value`，其中 `value` 设置为表示警告的颜色。默认值为 `echo -e` 输出的 ANSI 序列，将颜色设置为黄色。
- `SETCOLOR_NORMAL=value`，其中 `value` 设置为“正常”颜色。默认值为 `echo -e` 输出的 ANSI 序列。
- `LOGLEVEL=value`，其中 `value` 设置内核的初始控制台日志级别。默认值为 7；8 表示所有（包括调试）；1 表示除了内核崩溃外什么都不记录。`syslog` 在启动后将会覆盖此设置。
- `PROMPT=value`，其中 `value` 为以下布尔值之一：
  - 启用交互模式键。
  - 禁用交互模式键。

## /etc/sysconfig/iptables

`/etc/sysconfig/iptables` 文件存储内核在启动时或每次服务启动时设置数据包过滤服务的信息。除非您熟悉如何构建 `iptables` 规则，否则不应修改此文件。如果您没有运行 X 服务器，添加规则简单的方法是在终端提示符中使用 `/usr/sbin/lokkit` 命令。如果您正在运行 X 服务器，可以在终端提示符输入 `system-config-securitylevel`，或者从主菜单选择“应用程序” -> “系统设置”来启动图形化应用程序创建防火墙。使用这些应用程序会在过程结束时自动编辑此文件。

如果您愿意，可以使用 `/sbin/iptables` 手动创建规则，然后输入 `/sbin/service iptables saves` 将规则添加到 `/etc/sysconfig/iptables` 文件中。一旦该文件存在，保存的任何防火墙规则将在系统重启或服务重启后持续。

> 交叉引用：有关 `iptables` 的更多信息，请参第 34 章。

## /etc/sysconfig/irda

`/etc/sysconfig/irda` 文件控制系统中红外设备在启动时的配置。可以使用以下值：

- `IRDA=value`，`value` 为以下布尔值之一：
  - `yes` — 将运行 `irattack`，定期检查是否有设备尝试连接红外端口，例如另一台笔记本电脑尝试建立网络连接。为了让红外设备在您的系统中工作，此行必须设置为 `yes`。
  - `no` — 不运行 `irattack`，防止红外设备通信。
- `DEVICE=value`，`value` 是处理红外配置的设备（通常是串口）。
