
`5:initdefault:`

在此示例中，Ubuntu 启动到运行级别 5，这是一个启用网络的多用户模式，带有活跃的 X 会话和图形登录。该值被传递给 `/etc/init.d` 目录下的 `rc` 脚本。该脚本在启动或更改运行级别时使用；当您在启动过程中按 `i` 以“交互”模式启动 Ubuntu 时，它也充当解释器。

此时，init 使用与默认运行级别匹配相应的 `/etc/inittab` 条目。使用上一个例子，`/etc/inittab` 中的行将是：

```
5:wait: /etc/rc 5
```

`/etc` 目录下有一系列对应于每个运行级别的目录：

```
rc0.d rc2.d rc4.d rc6.d

rc1.d rc3.d rc5.d rcS.d
```

假设值为 1，`rc` 脚本将执行 `/etc/rc.1` 目录下的所有脚本，然后启动图形登录。

例如，如果 Ubuntu 启动到运行级别 1，则将执行以字母 K 开头的脚本，随后是 `/etc/rc1.d` 目录下以该字母开头的脚本：

```
# ls /etc/rc1.d/

K01gdm K19hplip K20laptop-mode K20vsftpd K80slapd

K01usplash K20acpi-support K20makedev K21acpid K86pppp

...etc...

K19cupsys K20inetutils-inet K20ssh K74-blue-utils S20single
```

这些脚本实际上是指向 `/init.d` 目录下系统服务脚本的符号链接。

`rc1.d` 文件带有字母和数字前缀，例如 `K15` 或 `$10`。前缀中的 `(K)` 或 `(S)` 表示是否应该杀死 `(K)` 或启动 `(S)` 特定的服务，并传递一个值来按顺序或启动相应的 `/etc/init.d` 脚本。前缀中的数字按特定顺序执行 `/etc/init.d` 脚本。符号链接有助于区分它们启动的顺序。启动时没有什么是绝对的，但某些服务需要在其他服务启动之前运行。你不会希望你的 Ubuntu 系统在先启动网络和 NFS 服务的情况下尝试挂载远程网络文件系统 `(NFS)` 卷。

# 使用 GRUB 启动到非默认运行级别

在选择默认运行级别后，每次从关机状态重启系统时，都会选择该运行级别。可能会有某些时刻你不想启动到该运行级别。你可能想要进入维护模式，或者在没有活跃 X 服务器和图形登录的情况下启动系统，以便修改或修复 X 服务器或桌面管理器。如果你使用 Ubuntu 的引导程序 `GRUB`，则需要遵循几个步骤启动到非默认运行级别。

> 如果你启用了 `GRUB` 密码，必须先按 `p`，输入密码，然后按 `Enter` 使用此启动方法。

`GRUB` 引导加载程序在启动时向内核传递参数或命令。这些参数等用于告诉 `GRUB` 内核所在的位置，并向内核传递特定参数，例如内存的可用情况或如何配置特殊硬件。

要覆盖默认运行级别，你可以按照如下方式为 `GRUB` 添加额外的内核参数：

在图形启动界面上，按 `e`（编辑），向下滚动选择内核，再次按 `e`。

按空格键，输入 `single 1`（Ubuntu 也允许使用 `S` 和 `s`），然后按 `Enter`。最后，按 `b` 启动，你将启动到运行级别 1，而不是 `/etc/initstab` 列出的默认运行级别。

# 理解 init 脚本和初始化的最后阶段

每个 `/etc/init.d` 脚本（或 init 脚本）包含确定接收到启动或停止值时执行操作的逻辑。该逻辑可能是用于执行的简单 `switch` 语句，例如所示：

```
case "$1" in

start)

  start

  ;

stop)

  stop

  ;

restart)

  restart

  ;

reload)

  reload

  ;

status)

  status

  ;

restart)

  restart

  ;

*)

  echo "Usage: $0 {start|stop|restart|reload|status}"

  exit 1

esac
```
