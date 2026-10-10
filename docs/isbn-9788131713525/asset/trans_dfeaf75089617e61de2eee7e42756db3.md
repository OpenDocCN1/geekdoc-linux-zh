
以这种方式在内核命令行中指定 `init=`，你就必须在根文件系统的 `/sbin` 目录中提供一个名为 `myinit` 的二进制可执行文件。这将是内核启动过程完成后获得控制权的第一个进程。

## 6.3 初始化进程

除非你正在做非常规的事情，否则你永远不会需要提供定制的初始进程，因为标准 `init` 进程的功能非常灵活。`init` 程序与我们稍后研究的启动脚本一起，实现了通常被称为*System V Init* 的系统，这源于使用此架构的原始 UNIX System V。我们现在将研究这个强大的系统配置和实用工具。

在上一节中，我们看到 `init` 是内核在启动过程完成后生成的第一个用户空间进程。正如你将了解到的，正在运行的 Linux 系统中的每个进程都与系统中运行的另一个进程具有子进程与父进程的关系。`init` 是 Linux 系统中所有用户空间进程的终极父进程。此外，`init` 为所有其他进程提供默认的继承环境参数集，包括诸如 `PATH` 和 `CONSOLE` 等参数。

其主要角色是在特殊配置文件的指导下生成额外的进程。此配置文件通常存储为 `/etc/inittab`。

`init` 具有*运行级别*的概念。运行级别可以被视为一种系统状态。每个运行级别由进入该运行级别时启用的服务和生成的程序定义。

在任意给定时刻，`init` 只能处于单个运行级别中。`init` 使用的运行级别包括从 0 到 6 的运行级别以及一个称为 S 的特殊运行级别。运行级别 0 指示 `init` 停止系统，而运行级别 6 会导致系统重启。对于每个运行级别，通常提供一组启动和关闭脚本，定义系统在每个运行级别应采取的操作。要针对给定运行级别执行的操作由稍后描述的 `/etc/inittab` 配置文件确定。

在许多发行版中，有几个运行级别被保留用于特定用途。表 6-2 详细列出了在大多数 Linux 发行版中常见的运行级别及其用途。

### 表 6-2：运行级别

| 运行级别 | 用途 |
| :--- | :--- |
| 0 | 系统关机（halt） |
| 1 | 用于维护的单用户系统配置 |
| 2 | 用户定义 |
| 3 | 通用多用户配置 |
| 4 | 用户定义 |
| 5 | 启动时带有图形用户界面的多用户模式 |
| 6 | 系统重启（reboot） |

运行级别脚本通常位于名为 `/etc/rc.d/init.d` 的目录下。在这里，你会找到大多数启用和禁用单个服务的脚本。可以通过调用脚本并向其传递适当的参数（例如 start、stop 或 restart）来手动配置服务。清单 6-3 显示了重启 nfs 服务的示例。

### 清单 6-3：NFS 重启

```
$ /etc/rc.d/init.d/nfs restart
Shutting down NFS mountd:                             [  OK  ]
Shutting down NFS daemon:                               [  OK  ]
Shutting down NFS quotas:                               [  OK  ]
Shutting down NFS services:                              [  OK  ]
Starting NFS services:                                    [  OK  ]
Starting NFS quotas:                                      [  OK  ]
Starting NFS daemon:                                      [  OK  ]
Starting NFS mountd:                                      [  OK  ]
```

如果你曾使用过 Red Hat 或 Fedora 等桌面 Linux 发行版，你一定在系统启动期间看到过类似的行。

运行级别由在该运行级别启用的服务定义。大多数 Linux 发行版在 `/etc` 下包含一个目录结构，其中包含指向 `/etc/rc.d/init.d` 中服务脚本的符号链接。这些运行级别目录通常以 `/etc/rc.d` 为根。在此目录下，你会找到一系列运行级别目录，包含每个运行级别的启动和关闭规范。`init` 只需在进入和退出运行级别时执行这些脚本。脚本定义了系统状态，inittab 指示 init 将哪些脚本与给定运行级别关联。清单 6-4 包含了 `/etc/rc.d` 下方的目录结构，该结构分别驱动指定运行级别进入和退出时的运行级别启动和关闭行为。

### 清单 6-4：运行级别目录结构

```
$ ls -l /etc/rc.d
total 96
drwxr-xr-x 2 root root 4096 Oct 20 10:19 init.d
-rwxr-xr-x 1 root root 2352 Mar 16 2004 rc
drwxr-xr-x 2 root root 4096 Mar 22 2005 rc0.d
drwxr-xr-x 2 root root 4096 Mar 22 2005 rc1.d
drwxr-xr-x 2 root root 4096 Mar 22 2005 rc2.d
drwxr-xr-x 2 root root 4096 Mar 22 2005 rc3.d
drwxr-xr-x 2 root root 4096 Mar 22 2005 rc4.d
drwxr-xr-x 2 root root 4096 Mar 22 2005 rc5.d
-rwxr-xr-x 1 root root 949 Dec 31 16:36 rc.local
-rwxr-xr-x 1 root root 2559 Jan 11 2005 rc.sysinit
```

每个运行级别由包含在 rcN.d 中的脚本定义，其中 N 是运行级别。在每个 rcN.d 目录中，你会找到许多按特定顺序排列的符号链接。这些符号链接以 K 或 S 开头。以 S 开头的指向使用启动指令调用的服务脚本；以 K 开头的指向使用关闭指令调用的服务脚本。一个包含很少服务的示例可能如清单 6-5 所示。

### 清单 6-5：示例运行级别目录

```
lrwxrwxrwx 1 root root 17 Nov 25 2004 S10network -> ../init.d/network
lrwxrwxrwx 1 root root 16 Nov 25 2004 S12syslog -> ../init.d/syslog
lrwxrwxrwx 1 root root 16 Nov 25 2004 S56xinetd -> ../init.d/xinetd
lrwxrwxrwx 1 root root 16 Nov 25 2004 K50xinetd -> ../init.d/xinetd
lrwxrwxrwx 1 root root 16 Nov 25 2004 K88syslog -> ../init.d/syslog
lrwxrwxrwx 1 root root 17 Nov 25 2004 K90network -> ../init.d/network
```

在这个例子中，我们指示启动脚本在进入这个假设的运行级别时启动三个服务：network、syslog 和 xinetd。由于 S* 脚本带有数字标记并有序，它们将按此顺序启动。类似地，当退出此运行级别时，将终止三个服务：xinetd、syslog 和 network。以类似的方式，这些服务将按照符号链接文件名中 K 后面的两位数顺序终止。在实际系统中，肯定会有更多条目。你也可以包含自己自定义应用程序的条目。

执行这些服务启动和关闭脚本的顶层脚本在 init 配置文件中定义，我们现在将研究它。

## 6.3.1 inittab

当 init 启动时，它读取系统配置文件 `/etc/inittab`。此文件包含每个运行级别的指令，以及适用于所有运行级别的指令。大多数 Linux 工作站上的手册页以及几本涵盖系统管理的书籍都对此文件和 init 的行为进行了详细记录。我们并不试图复制这些页面；我们专注于开发人员如何为嵌入式系统配置 inittab。若要详细了解 inittab 和 init 如何协同工作，请在大多数 Linux 工作站上输入 `man init` 和 `man inittab` 查看手册页。

让我们看看一个简单的嵌入式系统的典型 inittab。清单 6-6 包含一个简单的 inittab 示例，适用于支持单个运行级别以及关机和重启的系统。

### 清单 6-6：简单的 inittab 示例

```
# /etc/inittab

# 默认运行级别（在此例中为 2）
id:2:initdefault:

# 这是要运行的第一个进程（实际上是一个脚本）。
s1::sysinit:/etc/rc.sysinit

# 进入运行级别 0 时执行我们的关机脚本
10:0:wait:/etc/init.d/sys.shutdown

# 进入运行级别 2 时执行我们的正常启动脚本
12:2:wait:/etc/init.d/runlvl2.startup

# 此行执行重启脚本（运行级别 6）
16:6:wait:/etc/init.d/sys.reboot

# 此条目在控制台上生成一个登录 shell
# Respawn 意味着每次被终止时它都会重新启动
con:2:respawn:/bin/sh
```

这个非常简单的 inittab 脚本描述了三个独立的运行级别。每个运行级别都关联一个脚本，开发人员必须为每个运行级别的期望操作创建该脚本。当 *init* 读取此文件时，第一个执行的脚本是 `/etc/rc.sysinit`。这由 *sysinit* 标签表示。然后 *init* 进入运行级别 2，并执行定义为运行级别 2 的脚本。从这个例子来看，这将 是 `/etc/init.d/runlvl2.startup`。正如你可能从清单 6-6 中的 `:wait:` 标签猜到那样，*init* 会等待脚本完成后再继续。当运行级别 2 的脚本完成后，*init* 在控制台上生成一个 shell（通过 `/bin/sh` 符号链接），如清单 6-6 的最后一行所示。（*respawn* 关键字指示 *init* 每次检测到 shell 退出时都重新启动它。）清单 6-7 显示了启动期间的样子。

### 清单 6-7：启动消息示例

```
...
VFS: Mounted root (nfs filesystem).
Freeing init memory: 304K
INIT: version 2.78 booting
This is rc.sysinit
INIT: Entering runlevel: 2
This is runlvl2.startup
#
```

此例中的启动脚本除了为了说明目的而宣告自身之外什么也不做。当然，在实际系统中，这些脚本会启用执行有用工作的功能和服务！鉴于本例中的简单配置，你将在 `/etc/init.d/runlvl2.startup` 脚本中为你的特定小部件启用服务的应用程序，并执行相反操作——禁用你的
