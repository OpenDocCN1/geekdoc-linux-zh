
## init 进程

在传统的 V（SysV）风格 Linux 发行版中，`init`进程是第一个启动的非内核进程；因此，它总是获得进程 ID `1`。`init`读取其配置文件`/etc/inittab`，并确定它应该启动的运行级别（`runlevel`）。本质上，运行级别决定了系统的行为。每个级别（由 0 到 6 之间的整数指定）都有特定的用途。如果存在`initdefault`运行级别，则选择它；否则，系统会提示你选择一个运行级别。

`systemd` Linux 使用一个名为`systemd`的新启动管理器取代了以前由 SysV 提供的功能。在`systemd`中，运行级别的概念略有不同，被称为目标（`targets`）。第 8 章将更详细地讨论`systemd`。表 6-2 显示了传统 SysV 世界中不同的运行级别。

当`init`被指示进入某个运行级别时，它会根据`/etc/inittab`文件执行一个脚本。系统启动的默认运行级别由`/etc/inittab`文件中的`-initdefault`条目决定。例如，如果文件中的条目是

```
id:3:initdefault:
```

这意味着系统将启动到运行级别 3。

| SysV init 运行级别 | systemd 目标 | 说明 |
|---|---|---|
| 0 | `poweroff.target`, `runlevel0.target` | 关机 |
| 1 | `rescue.target`, `runlevel1.target` | 进入单用户模式 |
| 2 | `runlevel2.target`, `multi-user.target` | 多用户模式，传统上不带网络文件系统 (`NFS`) |
| 3 | `multi-user.target`, `runlevel3.target` | 全多用户模式（正常） |
| 4 | `multi-user.target`, `runlevel4.target` | 未使用或用户定义 |
| 5 | `graphical.target`, `runlevel5.target` | 与运行级别 3 相同，但使用的是 X Window（图形）系统登录而非基于文本登录 |
| 6 | `reboot.target`, `runlevel6.target` | 重启系统 |
| emergency | `emergency.target` | 紧急 shell |

表 6-2 Sysd init 运行级别和 systemd 目标

但另一方面，如果文件中的条目是

```
id:5:initdefault:
```

这意味着系统将启动到运行级别 5，并且 X Window 子系统将带有图形界面运行。

> 注意：在类 Debian 系统（如 Ubuntu）上，`/etc/inittab`提供的功能被`/etc/init/rc-sysinit`文件取代了。`rc-sysinit .conf`文件用于指定系统启动时的默认运行级别。这是通过将`DEFAULT_RUNLEVEL`变量的值设置为所需的运行级别来实现的。Ubuntu 发行版的默认值为`env DEFAULT_RUNLEVEL=2`。

## rc 脚本

在上一节中，我们提到在基于 SysV 的发行版中，`/etc/inittab`指定了在运行级别变化时运行的脚本。这些脚本负责启动或停止特定于运行级别的服务。

由于可能需要管理的服务非常多，使用了资源控制（`rc`）脚本。在基于 SysV 的发行版中，主`rc`脚本负责为每个运行级别按正确的顺序调用相应的脚本。你可以想象，一个简单的脚本可能会变得极其难以控制！为了防止这种情况，使用了一个稍微复杂一点系统。

对于每个运行级别，在`rc.d`的命名方案中存在一个子目录，其中 X 是运行级别。例如，运行级别 3 的所有脚本都在`/etc/rc.d/3`中。

在运行级别目录中，指向`/etc/rc.d/init.d`或`/etc/init.d`目录下脚本的符号链接。符号链接没有使用在`/etc/rc.d/init.d`或`/etc/init.d`目录中的实际名称，如果脚本要启动服务，则前缀`S`；如果要停止（或杀死）服务，则前缀`K`。请注意这些字母是区分大小写的。你必须使用大写字母，否则启动脚本将无法识别它们。

在许多情况下，`*/init.d`目录指向的脚本是工作主体；它们执行启动和停止服务的实际过程。当运行`/etc/rc`时，它会按数字顺序调用每个脚本。它首先运行以`K`开头的脚本，然后运行以`S`开头的脚本。对于以`K`开头的脚本，会传递一个`stop`参数。同样，对于以`S`开头的脚本，会传递`start`参数。

让我们查看示例 Fedora 服务器的`/etc/rc.d/rc3.d`目录：

```
[root@fedora-server ~]# ls -l /etc/rc.d/rc3.d/

lrwxrwx-x.1 root root 20 Nov 4 21:32 K50netconsole -> ../init.d/netconsole

lrwxrwx-x.1 root root 17 Nov 4 21:32 K90network -> ../init.d/network
```

从示例输出可以看出，`K50netconsole`是`/etc/rc.d/rc3.d`目录中的文件之一（输出的第一行）。因此，当`K50netconsole`执行或调用时，实际执行的是以下命令：

```
# /etc/init.d/netconsole stop
```

同样，如果调用名为`-S99carpald`的文件，实际执行的是：

```
# /etc/init.d/carpald
```

## 编写自己的 rc 脚本

在管理 Linux 脚本并保持其运行的过程中，某些时刻你需要修改启动或停止脚本。你可以使用多种方法来实现这一点。

如果更改要在启动时生效且更改较小，你可以直接编辑`/etc/rc.d/rc.local`或`/etc/rc.local`脚本。该脚本在启动过程的最后运行——在所有启动脚本之后。

另一方面，如果你的添加更复杂，或需要在停止过程中显式停止，你应该向`/etc/rc.d/`或`/etc/rc*`目录添加脚本。该脚本应该接受`start`和`stop`参数并采取相应操作。

当然，第一种方案`rc.local`脚本是两者中简单的。要向此脚本添加内容，只需用编辑器打开它并附加你想运行的命令即可。

如，如果你的情况需要更复杂或更优雅的解决方案，你需要创建一个独立的脚本并以此作为骨架。

## 第 6 章 启动与关机 171

4. 将脚本复制或移动到你的启动脚本可以找到它的目录；我们将使用`/usr/local/sbin/`目录：
`[root@fedora-server ~]# mv carpald.sh /usr/local/sbin/`

5. 注意`carpald.sh`脚本引用了`mailx`命令（见最后一行）。因此，你需要在系统上可用或安装`mailx`备用程序，以便在脚本中使用它。
在我们的示例 Fedora/CentOS/RHEL 系统上，你可以使用`dnf`来安装`mailx`——如果你还没有安装它的话。输入以下内容：
`[root@fedora-server ~]# dnf -y install mailx`

如果你在像 Ubuntu 这样基于 Debian 的系统中没有`mailx`，你可以通过运行`apt-get`程序来安装它：
`master@ubuntu-server:~# sudo apt-get -y install mailutils`

![](img/9f6657924397c33f088db5321b751a83_196_0.png)

## 创建启动脚本

在这里，你将创建一个在系统启动和关机期间执行的实际脚本。你创建的文件将命名为`carpald`。该文件将启用`chkconfig`。这意味着，如果你愿意，可以使用`chkconfig`工具来控制程序启动和停止的运行级别顺序。这是一个非常实用且节省时间的功能。

- 1. 启动你喜欢的任何文本编辑器，并输入以下文本：

```bash
#!/bin/sh

#Carpald

#

#chkconfig:    35 99 01

# description: Carpald 是一个每 1 小时唤醒一次的程序，

# 提醒我们需要离开键盘休息，

# 否则我们将失去手腕的所有功能，并且余生中

# 无法再次打字。

# 加载函数库。

/etc/init.d/functions
```

```bash
[ -f /usr/local/sbin/carpald.sh ] || exit 0

# 查看我们是如何被调用的。

case $1 in

start)

echo "Starting carpald: "

/usr/local/sbin/carpald.sh &

echo "done"

touch /var/lock/subsys/carpald

;;

stop)

echo -n "Stopping carpald services: "
```
