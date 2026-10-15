

+   • sendmail 文件包含两个变量：DAEMON 和 QUEUE。如果将 DAEMON 变量设置为 yes，系统在启动时会以守护进程模式 (-bd) 启动 sendmail。QUEUE 告诉 sendmail 在两次队列运行之间等待多长时间 (-q)；默认值为一小时。

## SUSE 启动脚本

SUSE 的启动系统与 Red Hat 相似，至少在总体组织结构方面如此。然而，SUSE 的脚本组织良好、健壮且文档齐全。维护操作系统这一部分的人员值得一颗金星。

与 Red Hat 一样，init 在每个运行级别调用脚本 /etc/init.d/rc，并将新的运行级别作为参数提供。特定于软件包的脚本位于 /etc/init.d 目录中，其配置文件位于 /etc/sysconfig 中。对 SUSE 启动过程的优秀介绍可在 /etc/init.d/README 中找到。

尽管 SUSE 和 Red Hat 都将启动配置文件集中在 /etc/sysconfig 中，但该目录内的具体文件却大不相同。（其中一点是，SUSE 的文件通常注释良好。）你通过设置 shell 环境变量来调用选项，然后 /etc/init.d 中的脚本会引用这些变量。某些子系统需要的配置比其他子系统多，需要多个配置文件的子系统拥有私有子目录，例如 sysconfig/network 目录。

windowmanager 文件是 sysconfig 目录中的一个典型示例：

```
## Path:          Desktop/Window manager
## Type:          string(gnome,startkde,startkde3,startxfce4,twm)
## Default:       kde
## Config:        profiles,kde,susewm

# Here you can set the default window manager (kde, fvwm, ...)
# changes here require at least a re-login

DEFAULT_WM="gnome"

## Type:           yesno
## Default:        yes

# install the SuSE extension for new users
# (theme and additional functions)

INSTALL_DESKTOP_EXTENSIONS="yes"

## Path:           Desktop
## Description:    default mouse cursor theme
## Type:           string
## Default:

# Name of mouse cursor theme for X11. Possible themes can be found
# in /usr/share/icons/

X_MOUSE_CURSOR="DMZ"
KDE_USE_IPV6="yes"
```

每个变量前面都有 YaST 可读的³ 配置信息和对变量用途的详细描述。例如，在窗口管理器文件中，变量 DEFAULT_WM 设置 X 使用的桌面窗口管理器。

SUSE 还包含一个 chkconfig 命令用于管理启动脚本。它与 Red Hat 提供的版本完全不同，但仍然是一个有效的工具，应优先于手动脚本管理使用。

## Ubuntu 启动脚本和 Upstart 守护进程

从 2007 年初的 Feisty Fawn 开始，Ubuntu 用 Upstart 取代了传统的 init，Upstart 是一个事件驱动的服务管理系统，也被一些其他 Linux 发行版使用。Upstart 处理系统状态转换——例如硬件更改——比 init 更优雅。它还显著减少了启动时间。

Upstart 根据系统事件（如设备添加或网络驱动器断开）启动和停止服务。为兼容性考虑，它也模拟了 init 的传统运行级别。然而，启动和关闭脚本的处理方式与 init 使用的方式有所不同。

Upstart 使用 /etc/event.d 目录中的作业定义文件，而不是 inittab 文件。作业在概念上类似于启动脚本：它执行一系列命令，然后将控制权返回给 Upstart。Ubuntu 系统上的作业集合如下所示：

```
ubuntu$ ls /etc/event.d
control-alt-delete last-good-boot logd rc0 rc1 rc2 rc3 rc4 rc5 rc6
rc-default rc5 rc5-sulogin sulogin tty1 tty2 tty3 tty4 tty5 tty6
```

随着时间的推移，更多的启动脚本将被转换为原生的 Upstart 作业。目前，Upstart 使用运行级别模拟脚本来启动系统。例如，rc2 脚本执行 /etc/rc2.d/rc，后者运行运行级别 2 的所有启动脚本。

由于需要保持这种兼容性，Ubuntu 管理员应使用 Ubuntu 的 update-rc.d 命令来维护 rc 目录中启动脚本的链接。语法为

```
update-rc.d service { start | stop } sequence runlevels .
```

update-rc.d 接受一个序列号（启动脚本应运行的顺序）和适用的运行级别作为参数。使用终止点来结束解析。

在运行级别转换期间稍后启动的服务，在系统退出该级别时应更早停止。例如，如果 CUPS 在启动时的序列值为 80，则在关机过程中应以大约 20 的序列值停止。添加适当链接的 update-rc.d 命令为

