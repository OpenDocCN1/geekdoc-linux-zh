
## 使用 UNIX SysV 系统初始化进程

大多数现代 Linux 系统中使用两种 SysV 系统初始化进程：传统的 SysV 系统初始化进程和 upstart 系统初始化进程。在这两种系统中，init 守护进程会运行一系列脚本来启动系统中的其他守护进程，以提供系统服务，并最终允许用户登录和使用系统。此外，init 守护进程还负责在系统初始化之后启动和停止守护进程，包括在系统停机或重启前停止守护进程。

### 运行级别

由于 init 守护进程通常一次需要管理多个守护进程，因此它根据系统将状态划分为运行级别（runlevels）。**运行级别**定义了加载到内存中并由特定系统的内核执行的守护进程的数量和类型。在任何时刻，Linux 系统可能处于表 8-3 中定义的七个标准运行级别中的任意一个。

![](img/c27875544958897d817484d558c208c8_389_0.png)

由于 init 守护进程负责启动和停止守护进程，从而改变运行级别，因此运行级别通常也被称为**初始化状态**（initstates）。

要查看系统的当前运行级别以及上一个运行级别（如果自系统启动以来运行级别已更改），可以使用 **runlevel** 命令，如下所示的输出：

```bash
[root@server1 ~]# runlevel
N 5
[root@server1 ~]# _
```

| 运行级别 | 常用名称 | 描述 |
| :--- | :--- | :--- |
| 0 | 停机 | 系统中没有正在内存中运行的守护进程，并且准备关机。 |
| 1 | 单用户 | 单用户模式 | 系统仅包含足够的守护进程，允许一个用户（root 用户）登录并执行系统维护任务。 |
| 2 | 多用户模式 | 系统运行大多数守护进程，并允许多个用户登录和使用系统服务。除了专用网络服务之外，大多数常见的网络服务在此运行级别也可用。 |
| 3 | 扩展多用户模式 | 系统具有与多用户模式相同的能力，但启动了所有额外的网络服务（例如，SNMP、NFS）。 |
| 4 | 未使用 | 通常未使用，但可以自定义以适合您的需求。 |
| 5 | 图形模式 | 系统具有与扩展多用户模式相同的能力，但带有图形登录程序。在使用 GNOME 桌面的系统中，该程序称为**GNOME 显示管理器（gdm）**，并在 tty1 或 tty7 上启动以允许图形登录。 |
| 6 | 重启 | 用于重启系统的特殊运行级别。 |

**表 8-3** Linux 运行级别

前述 runlevel 命令指示系统处于运行级别 5，并且进入此运行级别之前的最近一个运行级别是不存在的（N）。

要在正在运行的系统上更改运行级别，只需指定新的运行级别并跟随 **init** 命令即可；若要执行系统维护任务而从运行级别 5 更改为运行级别 1，可以使用以下命令：

```bash
[root@server1 ~]# runlevel
N 5

[root@server1 ~]# init 1
```

> *当系统进入单用户模式时，由 init 守护进程停止的守护进程列表。*

告知 INIT 进入单用户模式。

```bash
[root@server1 /]# 
[root@server1 /]# runlevel
5 1
[root@server1 /]# _
```

![](img/c27875544958897d817484d558c208c8_390_0.png)

在更改运行级别时，可以使用 **telinit** 命令替代 init 命令。因此，可以使用命令 **telinit 1** 来切换到单用户模式。

你还可以从引导加载器向 Linux 内核传递选项，以强制系统启动到特定的运行级别。如果在 GRUB/GRUB2 配置界面内的内核行末尾添加关键字 **single**，系统将启动到单用户模式。类似地，你可以通过在 LILO 引导提示符处输入 Linux 映像名称后跟随 **1**、**S**、**s** 或 **single** 来从 LILO 引导到单用户模式。

## /etc/inittab 文件

除非另有指定，否则 init 守护进程进入 /etc/inittab 文件中指定的默认运行级别。过去，/etc/inittab 文件包含 init 守护进程的整个配置。然而，在现代系统中，/etc/inittab 通常只包含一行未注释的代码，用于配置默认运行级别，如下所示：

```bash
[root@server1 ~]# cat /etc/inittab
id:5:initdefault:
[root@server1 ~]# _
```

/etc/inittab 文件中的行 **id:5:initdefault:** 告知 init 守护进程，运行级别 5 是在系统启动时初始化 Linux 系统时要启动的默认运行级别。

![](img/c27875544958897d817484d558c208c8_390_1.png)

在安装了图形用户界面环境的大多数 Linux 发行版中，运行级别 5 是默认运行级别。

Ubuntu Server 14.04 默认不包含 /etc/inittab 文件，但如果存在该文件，它会使用它来设置默认运行级别。相反，Ubuntu Server 14.04 的默认运行级别通常在 /etc/init/rc-sysinit.conf 文件中设置。

### 运行时配置脚本

在引导过程中，init 守护进程必须执行多个脚本来准备系统、启动守护进程，并最终使系统达到可用状态。这些脚本被称为**运行时配置（rc）脚本**。

在使用传统 UNIX SysV 系统初始化进程的 Linux 系统中，init 守护进程识别 `/etc/inittab` 文件中的默认运行级别，然后依次执行 `/etc/rc[runlevel].d` 目录中以 S 或 K 开头的文件。如果默认运行级别是 5，则 init 守护进程将按照字母顺序执行 `/etc/rc5.d` 目录中所有以 S 或 K 开头的文件。S 或 K 分别表示在进入此运行级别时是启动（Start）还是终止（Kill/stop）守护进程。`/etc/rc5.d` 目录的一些示例内容显示在以下输出中：

```bash
[root@server1 ~]# ls /etc/rc5.d
README          S20screen-cleanup    S91apache2
S15bind9        S20zfs-mount         S92tomcat7
S19postgresql   S20zfs-share         S99grub-common
S20postfix      S70dns-clean         S99ondemand
S20sysync      S70pppd-dns          S99rc.local
[root@server1 ~]# _
```

根据前述输出，你可以看到 init 守护进程在进入此运行级别时会启动 postfix 守护进程（S20postfix）。为了确保前述目录中的文件按特定顺序执行，在文件名开头的 S 或 K 之后会添加一个序列号。因此，文件 S19postgresql 总是先于文件 S20postfix 执行。

回想一下，运行级别 1（单用户模式）仅包含足够让单个用户登录并执行系统任务的守护进程。如果用户告知 init 守护进程使用 `init 1` 命令更改为此运行级别，则 init 守护进程将执行 `/etc/rc1.d` 目录中所有以 S 或 K 开头的文件。由于单用户模式下启动的守护进程较少，因此该目录中的大多数文件以 K 开头，如下所示的输出：

```bash
[root@server1 ~]# ls /etc/rc1.d
K08tomcat7     K20screen-cleanup    K80iptables   S70dns-clean
K09apache2     K20zfs-mount         K85bind9       S70pppd-dns
K20postfix     K20zfs-share        README          S90single
K20sysync      K21postgresql       S30killprocs
[root@server1 ~]# _
```

`/etc/rc[runlevel].d` 目录中的每个文件都只是一个指向 `/etc/init.d` 目录中可执行 rc 脚本的符号链接，根据符号链接文件名是以 S（启动）还是 K（终止/停止）开头，可以用来启动或停止特定的守护进程。

图 8-5 说明了对于启动到运行级别 5 的系统，传统的 UNIX SysV 系统初始化过程。

![](img/c27875544958897d817484d558c208c8_391_0.png)

> 一些 Linux 发行版使用 `/etc/rc.d` 目录替代 `/etc/rc[runlevel].d`，并使用 `/etc/rc.d/init.d` 目录替代 `/etc/init.d`。

![](img/c27875544958897d817484d558c208c8_392_0.png)

在使用 upstart 初始化系统的 Linux 系统中，不使用 `/etc/rc[runlevel].d` 目录。相反，init 守护进程识别 `/etc/inittab` 文件中的默认运行级别，然后直接执行 `/etc/init.d` 目录中的 rc 脚本，根据 `/etc/init` 目录中配置文件内指定的信息来启动或停止相应的守护进程。`/etc/init` 目录中的每个守护进程都有一个单独的配置文件，该文件使用标准通配符标记来识别应该启动或停止它的运行级别。例如，接下来显示的 `/etc/init/cron.conf` 文件表明，cron 守护进程应该在运行级别 2、3、4 和 5 ([2345]) 中启动，并且不应该在运行级别 2、3、4 和 5 ([12345]) 中停止（注：原文此处逻辑表述可能存在笔误，通常停止指令对应不同的级别，但此处按原文翻译）：

```bash
[root@server1 ~]# cat /etc/init/cron.conf
# cron - regular background program processing daemon
#
# cron is a standard UNIX program that runs user-specified programs at
# periodic scheduled times
description     "regular background program processing daemon"
start on runlevel [2345]
stop on runlevel [12345]

expect fork
respawn

exec cron
[root@server1 ~]# _
```

图 8-6 说明了对于启动到运行级别 5 的系统，upstart 系统初始化过程。

![](img/c27875544958897d817484d558c208c8_392_1.png)

一些守护进程与 upstart 初始化系统不兼容。因此，使用 upstart 初始化系统的 Linux 发行版通常会托管几个传统的 UNIX SysV 守护进程，这些守护进程是通过 `/etc/rc[runlevel].d` 目录中的条目启动的。

