
# Linux 启动与 init 服务管理

Linux 启动后，它会运行一个名为 `init` 的程序。`init` 命令负责在计算机上启动、重启或停止服务。虽然不同的 Linux 发行版在 `init` 命令管理服务的方式上有所不同，但所有发行版都使用某种形式的相互依赖的 shell 脚本（其中许多是符号链接），这些脚本以特定的顺序响应特定的系统状态或运行级别（`runlevel`）而被调用。

你可以通过使用 `pstree` 命令或显示进程之间关系的其他实用程序，来查看 `init` 命令如何负责在 Linux 下启动进程。例如，使用 `pstree` 命令可能会返回以下结果：

```
init-->alarmd
    |-artsd
    |-atd
    |-cron
    |-gpm
    |
    |-in.identd--in.identd--3*[in.identd]
    |-inetd
    |-10*[kdeinit]
    |-kdeinit--kdeinit
            |
            |-kdeinit--bash--telnet
            |
            |-2*[kdeinit--bash
            |
            |-kdeinit--bash--bash
            |
            |
            '------------'-pstree
            '---2*[netscape--netscape]
    ...
```

此示例在 SuSE Linux 系统上运行，表明 `init` 负责启动各种程序，例如调度、控制台鼠标控制以及 KDE。请注意，并非所有输出都会显示，因为系统初始启动时可能会启动许多其他服务。在一个已启动到图形登录界面并等待用户开始工作的 `LinuxPPC 2000` 系统上，可以看到以下输出：

```
$ pstree
init--\atd
    |-automount
    |-cron
    |-gdm-+-X
    |     |-gdm--gdmlogin
    |-gpm
    |-httpd--8*[httpd]
    |-identd--identd--3*[identd]
    |-inetd--in.telnetd--login--bash--pstree
    |-kflushd
    |-khubd
    |-klogd
    |-kpiod
    |-kswapd
    |-kupdated
    |-lpd
    |-6*[mingetty]
    |-portmap
    |-rclick
    |-rpc.statd
    |-sendmail
    |-syslogd
    `-xfs
```

这里可以看到各种服务已启动。但 `init` 命令是如何启动这些服务的呢？理解 Linux 如何启动这些服务以及不同运行级别（`runlevel`）之间的关系，有助于你在启动时诊断问题，或有助于克服初始化硬件设备（如网络接口卡）时的问题。

## 运行级别简介

例如，当你直接将 `LinuxPPC 2000 Q4` 启动到运行 `X Window System` 的图形登录界面时，Linux 已启动到运行级别 `5`，该级别支持多用户、多任务、网络操作和 X 窗口系统。相反，在 SuSE Linux PPC 系统上，此运行级别被指定为运行级别 3！无论编号方案如何（如系统初始化表中所述），所有 Linux 系统通过 `/etc/inittab` 启动服务的方式大致相同。例如，在 LinuxPPC 2000 Q4 下，运行级别定义如下：

```
# Default runlevel. The runlevels used by RHS are:

# 0 - halt (Do NOT set initdefault to this)

# 1 - Single user mode

# 2 - Multiuser, without NFS (The same as 3, if you do not have networking)

# 3 - Full multiuser mode

# 4 - unused

# 5 - X11

# 6 - reboot (Do NOT set initdefault to this)
```

如你所见，你的 Linux 系统在关机时处于运行级别 0，在重启时处于运行级别 6，或在启动时处于 1、2、3 或 5。运行级别 1，即维护模式，通常由 root 操作员用于主要维护操作。这个运行级别很少使用，除非在启动过程中出现问题，否则很少会遇到（请记住，大多数 Linux 用户旨在让系统尽可能长时间保持运行状态）。在 SuSE Linux 中，运行级别定义如下：

```
# /sbin/init.d/rc takes care of runlevel handling

#

# runlevel 0 is halt

# runlevel S is single-user

# runlevel 1 is multi-user without network

# runlevel 2 is multi-user with network

# runlevel 3 is multi-user with network and xdm

# runlevel 6 is reboot
```

这些运行级别对应于 `/etc/rc.d/`（对于基于 Red Hat 的系统）或 `/sbin/init.d`（对于 SuSE Linux）目录下的目录，其中包含带编号的脚本。主要控制脚本位于 `init.d` 目录下。例如，在基于 Red Hat 的系统中，目录结构如下所示：

```
$ ls /etc/rc.d
init.d  rc.local  rc.sysinit  rc1.d  rc3.d  rc5.d
rc      rc.news   rc0.d       rc2.d  rc4.d  rc5.d
```

请注意，`rc_X.d` 目录对应于运行级别 `x`（0 到 6）。在每个 `rc_X.d` 目录下，你会发现指向 `init.d` 目录下脚本的符号链接，这些脚本根据运行级别控制特定的进程、服务或软件包。例如，当 Linux 启动到运行级别 3（使用仅文本控制台的系统状态）时，`/etc/rc.d/rc3.d` 到 `/etc/rc.d/init.d` 脚本的符号链接将被使用：

```
K83ypbind --> ../init.d/ypbind

K84ypserv --> ../init.d/ypserv

K92anacron --> ../init.d/anacron

K92ipchains --> ../init.d/ipchains

K96irda --> ../init.d/irda

S10network --> ../init.d/network

S11portmap --> ../init.d/portmap

S14nfslock --> ../init.d/nfslock

S18autofs --> ../init.d/autofs

S20random --> ../init.d/random

S25netfs --> ../init.d/netfs
```

请注意，并非所有链接都列在这里。但链接的名称很重要，链接执行的顺序也很重要。以 K 开头的名称表示要停止的服务，而以 S 开头的名称表示要启动的服务。名称中的数字决定了在切换到该运行级别时动作发生的时间。上述运行级别 3 的文件表明，当 Linux 系统处于特定状态（如启动、重启或关机）并进入特定运行级别时，正确的脚本组将按照特定的正确顺序执行（尽管许多基于 Red Hat Linux 的系统在继续使用 PCMCIA 服务时，会继续启动，然后延迟网络连接；更好的方法是先启动 PCMCIA，然后启动网络服务）。

在 Linux 执行完各种脚本后，其他服务可能会根据其他文件（如 Red Hat 系统中的 `/etc/sysconfig` 或 `/etc/rc.d/rc.local`，或 SuSE Linux 中的 `/etc/rc.config` 或 `/etc/rc.d/boot.local`）中的条目而启动或停止。直接在登录之前执行的初始化脚本是本地定制系统的理想位置，例如配置键盘按键以模拟鼠标按钮。

## 启动和停止服务

确定在 Linux 启动时启动哪些服务，通常由 `/etc` 目录下各种系统配置文件中嵌入的值决定。如前所述，SuSE Linux 使用名为 `rc.config` 的系统-wide 配置文件，该文件随后被名为 `suSeConfig` 的 shell 脚本轮询。这个 shell 脚本反过来重新配置系统，并自动为每个运行级别构建适当的依赖项和符号链接。

在 LinuxPPC 2000 和其他基于 Red Hat 的系统中，超级用户可以使用图形实用程序，如 `ntsysv`（基于控制台）或 `tksysv`（基于 X11）命令，来重新配置服务和运行级别。反过来，这些命令使用 `chkconfig` 命令重建脚本依赖项。
