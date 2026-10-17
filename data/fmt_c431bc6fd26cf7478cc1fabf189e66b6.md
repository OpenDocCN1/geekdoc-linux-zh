
`mount` 命令将文件系统加载到我们服务器的文件系统中。在这种情况下，设备是软磁盘驱动器（`/dev/fd0`），该设备的文件系统被加载到 `/media/floppy`——这就是挂载点。我们还需要告诉 Linux 期望在设备上找到什么类型的文件系统。在这种情况下，我们正在使用格式化为 `FAT32` 的磁盘，并通过 `-t vfat` 指定了这一点。

让我们仔细观察一下这里发生着什么。我们正在使用一张来自旧 `Windows` 机器的软磁盘；该磁盘上存储了几个目录，如图 4.11 所示。

### 图 4.11。在 Windows 中查看软磁盘的文件系统。

![](img/9ba05966cc0c98b5830dd68d51d157c1_132_0.png)

正如我们在第 2 章中看到的，`Linux` 中没有 `A` 盘器；可移动介质设备显示为 `/media` 目录内文件系统的一部分。因此，当我们挂载软磁盘时，它会出现在 `/media/floppy` 目录下，如图 4.12 所示。

### 图 4.12。软磁盘的文件系统作为 Linux 文件系统的一部分显示。

![](img/9ba05966cc0c98b5830dd68d51d157c1_132_1.png)

## 使用 umount 命令卸载文件系统

在拔出软磁盘之前，我们应该先卸载它，从而将其从文件系统中移除。我们可以使用 `umount` 命令来实现这一点——注意这里少了一个字母“n”——如下所示。

```
[kermit@swinetrek ~]$ ummount /media/floppy
[kermit@swinetrek ~]$
```

对于某些设备来说，卸载过程非常重要。软磁盘就是一个很好的例子。向软磁盘保存文件可能需要很长时间；卸载过程可以确保所有向磁盘写入数据的程序在设备被移除之前完成它们的写入操作。

## 文件系统表 (fstab)

你服务器文件系统的许多配置选项都包含在一个单一文本文件 `/etc/fstab` 中。由于该文件对系统的运行至关重要，因此该文件的所有者是 `root`，只有 `root` 才能写入该文件。这种所有权权限结构防止了非 `root` 用户对文件进行任何潜在的灾难性修改或删除。强烈建议不要调整这些权限，并在登录 `root` 身份时对该文件给予应有的尊重。

## 编辑只读文件

![](img/9ba05966cc0c98b5830dd68d51d157c1_133_0.png)

以 `root` 身份编辑文本文件有很多方法。可能简单的方法是在切换到 `root` 用户后，从命令行启动你喜好的文本编辑器。文本编辑器将像你以 `root` 身份登录一样运行，因为 `GNOME` 将坚持向终端返回一个看起来难看的消息：

```
[kermit@swinetrek ~]$ su
Password:
[root@swinetrek ~]# edit /etc/fstab
```

```
(gedit:2066): GNOME-WARNING **: While connecting to session manager:
Authentication Rejected, reason : None of the authentication protocols specified are supported and host-based authentication failed.
```

## 文件系统表 (fstab)

使用这种方法编辑文件完全没有问题。`Kate` 或你选择的任何文本编辑器都可以正常运行。然而，如果你想消除这个警告，`Bruce Wilk` 在 `linux.redhat` 新闻组中建议了以下脚本作为解决方案。

```bash
#!/bin/sh

if [ $ -lt 1 ];
  then echo "usage: basename $0 command" >&2
  exit 2
fi

exec -c "exec env DISPLAY='$DISPLAY' \
  XAUTHORITY=${XAUTHORITY_HOME}/.xauthority \
  "$SHELL" -c '$*'
```

将此文件保存为 `xtroot.sh`，并放在你家目录下名为 `bin` 的目录中。你可能需要创建这个目录，还需要赋予自己该文件的执行权限。你可以通过运行 `chmod +x /bin/xtroot.sh`，或者在 `Nautilus` 中更改文件的权限来实现。

由于 `/home/username/bin` 自动包含在环境变量 `PATH` 中，你理应能够简单地通过输入 `xtroot.sh` 直接从命令行运行它。

```
[kermit@swinetrek -]$ xtroot.sh gedit
Password:
```

`fstab` 是 "filesystem table"（文件系统表）的缩写，它为操作系统提供了关于设备应该挂载在哪里的说明。

`/etc/fstab` 文件类似于：

```text
# This file is edited by fstab-sync see 'man fstab-sync' for
# details
/dev/VolGroup00/LogVol00 /ext3 defaults 1 1
LABEL=/boot /ext3 defaults 1 2
/dev/devpts /dev/pts devpts gid=5,mode=620 0 0
/dev/shm /dev/shm tmpfs defaults 0 0
/dev/proc /proc defaults 0 0
/dev/sys /sys defaults 0 0
/dev/VolGroup00/LogVol01 /media/floppy auto 0 0
```

## 系统管理

### 文件系统表 (fstab)

`rw` 文件系统提供读写访问。

`ro` 文件系统提供只读访问。

对于挂载设备和文件系统的许多其他选项，正如你在默认 `fstab` 文件中看到的，但这些是我们感兴趣的。在我们的示例中，许多选项被设置为 `defaults`。在 `Fedora Core` 系统中，这等同于 `auto, rw`。

5. 第五列用于 `dump` 工具判断是否将文件系统包含在备份中——0 值告诉 `dump` 忽略该文件系统。

6. 最后的一列指示是否由 `fsck`（文件系统检查）工具检查。`ext3` 文件系统很少受益于此类检查。如果你想进行此类检查，你应该按照你希望检查的顺序对文件系统进行编号——第一个 1，第二个 2，依此类推。

有了格式正确的 `fstab` 文件，使用 `mount` 命令将变得简单得多：

```
[kermit@swinetrek -]$ su
Password:
[root@swinetrek kermit]# mount /media/floppy
[root@swinetrek kermit]# exit
exit
[kermit@swinetrek -]$
```

在这里，我们只指定了挂载点。`mount` 查找 `fstab` 来识别与该挂载点相关的设备。

能否以普通用户身份挂载设备，取决于 `fstab` 中注的选项以及设备文件的权限。如果挂载点由 `root` 所有，而你尝试作为普通用户挂载它，你将看到“Permission denied”（权限被拒绝）错误。

## 创建挂载点

直到为止，我们只讨论了 `Fedora Core` 关于挂载点的惯例。其他 `Linux` 系统使用不同的惯例，以便挂载点名称更易识别。例如，`SuSE` 在安装系统时会创建一个 `/floppy` 挂载点，而不是 `Fedora` 的 `/media/floppy`。

# 第 4 章：系统管理

其他发行版可以使用不同的约定，这一事实应该告诉你挂载点的命名并不是标准的，也不应该是标准的。请记住，挂载点仅仅是系统上的另一个目录。如果你对正在使用的发行版所采用的约定感到困惑，请使用你偏好的约定。

例如，你可以在你的 `Fedora` 系统上使用上述 `SuSE` 约定：

```
kermit@swinetrek ~]$ su
Password:
root@swinetrek kermit]# mkdir /floppy
root@swinetrek kermit]# exit
kermit@swinetrek ~]$ mount -t vfat /dev/fd0 /floppy
kermit@swinetrek ~]$
```

在这里，我们将软盘的文件系统挂载到了一个新的挂载点：`/floppy`。我们可以通过编辑 `fstab` 来使此更改永久生效。

**文件：`/etc/fstab`**

```text
# 此文件由 fstab-sync 编辑 - 详情请参 man fstab-sync
#
/dev/VolGroup00/LogVol00 | | ext3 defaults | 1 1 |
LABEL=/boot | | /boot ext3 defaults | 1 2 |
/dev/devpts | /dev/devpts devpts gid=5,mode=620 0 0 |
/dev/shm | /dev/shm tmpfs defaults | 0 0 |
/dev/proc | /proc proc defaults | 0 0 |
/dev/sys | /sys sysfs defaults | 0 0 |
/dev/VolGroup00/LogVol01 | swap swap defaults | 0 0 |
/dev/fd0 | /floppy auto pamconsole,exec. noauto,managed 0 0 |
/dev/hdc | /media/cdrom auto pamconsole,exec. noauto,managed 0 0 |
```

现在我们只需输入 `mount /floppy` 即可挂载软盘。

## 自动挂载文件系统

我们可以使用 `fstab` 中的 `auto` 选项来使某些设备的挂载过程自动化。要为了在插入 `CD-ROM` 后自动挂载，请将 `/dev/hdc` 列出的选项从 `noauto` 改为 `auto`。

```text
# 此文件由 fstab-sync 编辑 - 详情请参阅 'man fstab-sync'
#
/dev/VolGroup00/LogVol00 / ext3 defaults 1 1
LABEL=/boot /boot ext3 defaults 1 2
/dev/devpts /dev/pts devpts gid=5,mode=620 0 0
/dev/shm /dev/shm tmpfs defaults 0 0
/dev/proc /proc defaults 0 0
/dev/sys /sys sysfs defaults 0 0
/dev/VolGroup00/LogVol01 swap auto 0 0
/dev/fd0 /media/floppy auto pamconsole,exec,
                                     noauto,managed 0 0
/dev/hdc /media/cdrom auto pamconsole,exec,
                                     auto,managed
```

现在，每当你插入 `CD-ROM` 时，它都会自动挂载。

## 服务

与每个现代操作系统一样，`Linux` 在后台有很多在运行。如果你是一个普通的电脑用户——在 `Linux`、`Mac` 或 `Windows` 系统上——你很少会有充分的理由与这些后台任务交互。大多数时候，你甚至不会察觉它们的存在。这些任务独立运行，只要你不干扰它们，它们就不会干扰你。即使作为管理员，你可能也不需要比启动、停止或重启这些服务之外做更多事情。但不要让缺乏直接接触误导了你：这些服务对于你系统的运行至关重要。

`Linux` 的系统服务通常被称为守护进程（`daemons`）。它们是在后台运行的应用程序，提供如文件和打印机共享、电源管理、自动任务调度和系统日志等关键功能。例如，你的 `Web` 服务器将运行 `httpd`，它是 `Apache` 核心的 `HTTP` 守护进程。如果你使用 `MySQL`，你还需要运行 `MySQL` 守护进程 `mysqld`。

## 服务配置工具

**图 4.13。服务配置工具。**

![](img/9ba05966cc0c98b5830dd68d51d157c1_139_0.png)

你可以通过选择 桌面 > 系统设置 > 服务器设置 > 服务 来启动服务配置工具，它可以用于停止和启动服务。该工具如图 4.13 所示。

要停止或启动服务，请从左面板列表中选择它。右侧将显示简要描述以及该服务的当前状态。要启动已停止的服务，点击窗口顶部的“Start”（启动）按钮；要停止运行的服务，点击“Stop”（停止）按钮。还有一个“Restart”（重启）按钮，可用于重启服务——此操作对于某些配置更改生效可能是必要的。

你还可以使用此工具配置服务在开机时自动启动。要这样做，请勾选服务名称旁的复选框，并点击“Save”（保存）。

## 服务与运行级别

运行级别（`Runlevels`）基本上是描述系统当前可用设施的一种方便方式。在运行级别 5 中，所有系统功能均可用：多个用户可以登录，网络功能可用，且 `GUI` 正在运行。随着系统的启动和系统功能的可用，会触发其他运行级别：

- 运行级别 1：一次只能有一个用户登录。没有网络资源可用。
- 运行级别 2：多个用户可以同时登录，但没有网络支持。
- 运行级别 3：与运行级别 2 相同，网络资源可用。
- 运行级别 5：除了运行级别 3 之外，`GUI` 也可用。

## 运行级别 4 发生了什么？

没有运行级别 4——这个是留给系统专家的。

![](img/9ba05966cc0c98b5830dd68d51d157c1_140.png)

# 第 4 章：系统管理

**图 4.14。编辑所有运行级别。**

![](img/9ba05966cc0c98b5830dd68d51d157c1_11.png)

服务配置工具允许你设置服务在运行级别 3、4 或 5 时启动。要更改给定的运行级别，从“Runlevel”菜单中选择选项。你可以一次编辑一个运行级别，也可以通过选择“All”（所有）来编辑全部，如图 4.14 所示。

勾选框框以指定你想自动启动的守护进程，当你想要停止守护进程时，点击窗口顶部的“Save”。注意，如果你想要守护进程在运行级别 3、4 和 5 ，你需要勾选所有。当系统达到运行级别 5 时，将会停止。

## 使用 service 启动和停止服务

要从命令行停止、启动或获取服务的状态，可以使用 `Fedora` 的 `service` 工具，它位于 `/sbin` 目录中。记住，如果你将 `/sbin` 添加到了环境变量，就不需要在命令前加 `/sbin/` 了。

```
kermit@swinetrek ~]$ su
Password:
root@swinetrek kermit]# /sbin/service status
httpd is stopped
root@swinetrek kermit]# /sbin/service start
Starting httpd: [ OK ]
root@swinetrek kermit]# /sbin/service status
httpd (pid 2928) is running...
root@swinetrek kermit]# /sbin/service stop
```

## 使用 nsysv 自动启动服务

```
Stopping httpd:
root@swinetrek kermit]# [ OK ]
exit
root@swinetrek kermit]# exit
kermit@swinetrek ~]$
```

该工具两个参数：守护进程名称（在本例中为 `httpd`）和要执行的操作。所有服务都支持 `start`、`stop`、`restart` 和 `status`。

## 使用 nsysv 自动启动服务

`ntsysv` 是一种特殊的命令行工具，因为它提供了类似于第 1 章中基于文本的安装界面，如图 4.15 所示。

**图 4.15。在终端运行 nsysv。**

![](img/9ba05966cc0c98b5830dd68d51d157c1_142.png)

默认情况下，`nsysv` 只编辑运行级别 5。你可以通过在启动 `nsysv` 时使用 `--level` 选项来更改。例如，`nsysv --level 3` 将编辑运行级别 3。

## 使用 chkconfig 自动启动服务

`chkconfig` 是 `nsysv` 更传统的命令行对应。

```
kermit@swinetrek ~]$ su
Password:
root@swinetrek kermit]# /sbin/chkconfig --level 345 httpd
root@swinetrek kermit]#
exit
kermit@swinetrek ~]$
```

此命令让 `httpd` 在级别 3、4 和 5 启动。运行 `chkconfig --list` 可以获取每个级别启动的服务列表。

## 自动化常规任务

计算机旨在为我们执行任务。我们计算生命的大部分时间都在重复地执行相同的任务，其中许多任务最终是相当无脑的。系统管理有时会变成一项充满单调和常规的事务：相同的按键、相同的检查、相同的结果。如果我们能把计算机投入预期用途，让它为我们做这些事情不是理想的吗？

`Linux` 提供了许多自动化任务的方法。脚本虽然有帮助，但真正的力量在于两个特定的设施：`cron` 和程度较小的 `at`。这些是你执行此类常规任务所需的工具，如存档日志、使用新安装应用程序更新系统数据库、写入服务器统计等。

## cron

`cron` 是一个执行调度脚本的 `Linux` 系统守护进程。`cron` 守护进程（或 `cron`）作为系统启动时启动的服务运行。它每分钟检查一次自己的调度数据库需要执行的任务。

`cron` 的核心是 `/etc/crontab` 文件，下方显示了未修改的 `Fedora Core` 安装内容：

```text
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
```
