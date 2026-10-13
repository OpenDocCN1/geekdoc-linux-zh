
```
/etc/rc.init.d/

acpid bpbd ip6tables keytable mars-nwe nfs

postgresql ripid smartest vcnserver zebra aep1000 bluetooth

FreeWnn ipchains killall mdmond nslfock provlic

ripnog sed vsftpd asd bootampr framework iptables

krop messagebox nscd psacct routed snmpd winbind

anacron canna gkrelltrap irda apmd krb524 microcode_ctl ntpd

pxe rstatad smnttrap xfs apmd cppraygard gpm

irbalance krb5kcd mysql osfd6 raidius rusersd

spassassin arvpatch crowd halt iscsi kuzdu

named ospfd rawvald squid ldap dentump pand

atalc cups hpojd isdn shedd vspasswd dadd dhcpcd

random rowhdd isicom lisa ndetmap-server pcmcia rapd

saslahtd syslog ypersov autds dhcreley indent kadmin

l_sensors netfs portmap rawdevices sendmail tux

tyfp bcm5820 dovecot innd kdcrate mailman

network postfix rhnsd single ups yum
```

`rc.d` 链接以字母开头，例如 `K15` 或 `S10`。这些前缀中的 `(K)` 或 `(S)` 表示特定服务应该被杀死 `(K)` 还是启动 `(S)`，并向 `/etc/rc.d/init` 脚本传递 `stop` 或 `start` 的值。前缀中的数字按特定顺序执行特定的 `/etc/rc.d/init` 脚本。符号链接必须界定它们启动的顺序。数字本身并没有规定，但某些服务需要在其他服务启动之前运行。例如，你不会希望你的 Fedora Core Linux 系统在没有启动网络和 NFS 服务的情况下尝试挂载远程网络文件系统 `(NFS)` 卷。

在我们当前运行级别的所有系统服务启动后，`init` 会启动图形登录（因为我们处于级别 5）。图形登录的定义出现在 `/etc/initabb` 的末尾，如下所示：

```
# Run xdm in runlevel 5

x5:respawn:/etc/X11/predfm -nodaemon
```

此示例显示名为 `xdm` 的 shell脚本在 Fedora Core Linux 启动到运行级别 5 时执行正确的 X11 显示管理器。

# 使用 GRUB 启动到非默认运行级别

选择默认运行级别后，每次从关机状态重启系统时都会选择该运行级别。某些时候你可能不想启动到运行级别。你可能需要进入维护模式，或者在没有活动 X 服务器和图形登录的情况下启动系统，以便修改或修复 X 服务器或桌面管理器。如果你为 Fedora 使用 GRUB 引导程序，需要遵循几个特定步骤启动到非默认运行级别。

> 注意
> 如果你启用了 GRUB 密码，在使用此启动方法之前，必须先按 `p`，输入密码，然后按回车。

GRUB 引导程序在启动时向内核传递参数或命令。这些参数等用于告诉 GRUB 内核所在的位置，并向内核传递特定参数，例如可用内存量或应如何配置特殊硬件。

若要覆盖默认运行级别，可以按照如下方式为 GRUB 添加额外的内核参数：

1. 在图形界面上，按 `e`（编辑），向下滚动选择内核，然后再次按 `e`。
2. 按空格键，输入 `single` 或 `t`（Fedora Core 也允许 `s` 和 `as`），然后按回车。
3. 最后，按 `b` 启动，你将进入运行级别 1 而不是默认运行级别。

`rc.d` 链接以字母开头，例如 `K15` 或 `S10`。这些前缀中的 `(K)` 或 `(S)` 表示特定服务应该被杀死 `(K)` 还是启动 `(S)`，并向 `/etc/rc.d/init` 脚本传递 `stop` 或 `start` 的值。前缀中的数字按特定顺序执行特定的 `/etc/rc.d/init` 脚本。符号链接必须界定它们启动的顺序。数字本身并没有规定，但某些服务需要在其他服务启动之前运行。例如，你不会希望你的 Fedora Core Linux 系统在没有启动网络和 NFS 服务的情况下尝试挂载远程网络文件系统 `(NFS)` 卷。在我们运行级别的所有系统服务启动后，`init` 会启动图形登录（因为我们处于级别 5）。图形登录的定义出现在 `/etc/initabb` 的末尾，如下所示：

```
# Run xdm in runlevel 5

x5:respawn:/etc/X11/predfm -nodaemon
```

此示例显示名为 `xdm` 的 shell脚本在 Fedora Core Linux 启动到运行级别 5 时执行正确的显示1管理器。

# 使用 GRUB 启动到非默认运行级别

选择默认运行级别后，每次从关机状态重启系统都会选择该运行级别。某些时候你可能不想启动到运行级别。你可能需要进入维护模式，或者在没有活动 X 服务器和图形登录的情况下启动系统，以便修改或修复 X 服务器或桌面管理器。如果你为 Fedora 使用 GRUB 引导程序，需要遵循几个特定步骤启动到非默认运行级别。

> 注意
> 如果你启用了 GRUB 密码，在使用此启动方法之前，必须先按 `p`，输入密码，然后按回车。

GRUB 引导程序在启动时向内核传递参数或命令。这些参数用于告诉 GRUB 内核所在的位置，并向内核传递特定参数，例如可用内存量或应如何配置特殊硬件。

若要覆盖默认运行级别，可以如下为 GRUB 添加额外的内核参数：

1. 在图形界面上，按 `e`（编辑），向下滚动选择内核，然后再次按 `e`。
2. 按空格键，输入 `single` 或 `t`（Fedora Core 也允许 `s` 和 `as`），然后按回车。
3. 最后，按 `b` 启动，你将进入运行级别 1 而不是默认运行级别。

`rc.d` 链接以字母开头，例如 `K15` 或 `S10`。这些前缀中的 `(K)` 或 `(S)` 表示特定服务应该被杀死 `(K)` 还是启动 `(S)`，并向 `/etc/rc.d/init` 脚本传递 `stop` 或 `start` 的值。前缀中的数字按特定顺序执行特定的 `/etc/rc.d/init` 脚本。符号链接必须界定它们启动的顺序。数字本身并没有规定，但某些服务需要在其他服务启动之前运行。例如，你不会希望你的 Fedora Core Linux 系统在没有启动网络和 NFS 服务的情况下尝试挂载远程网络文件系统 `(NFS)` 卷。在我们运行级别的所有系统服务启动后，`init` 会启动图形登录（因为我们处于级别 5）。图形登录的定义出现在 `/etc/initabb` 的末尾，如下所示：

```
# Run xdm in runlevel 5

x5:respawn:/etc/X11/predfm -nodaemon
```
