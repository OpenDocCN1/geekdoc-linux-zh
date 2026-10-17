
`x:5:respawn:/etc/X11/prefd -nodaemon`

此命令运行`/etc/X11/prefd`，它是指向特定显示管理器的符号链接。对于 GNOME 图形桌面（Red Hat Linux 的默认设置），`/etc/X11/prefd`是指向`/usr/bin/gdm`的符号链接——即 GNOME 显示管理器。如果你使用 KDE 作为默认桌面（Caldera 和 SuSE 发行版的默认设置），`/etc/X11/prefd`是指向`/usr/bin/kdm`的符号链接——即 KDE 显示管理器。这意味着无论你选择哪种 GUI，`init`都会在运行级别 5 启动显示管理器。显示管理器反过来显示图形登录框并允许你登录系统。

如果你在 Linux 安装期间（第 1 到第 3 节介绍）没有启用图形登录界面，可以通过编辑`/etc/inittab`文件来启用。找到包含`initdefault`的行，并确保其内容如下（两列之间的运行级别应该是 5）：

```
id:5:initdefault:
```

![](img/448aa2bd6846782b632c764b035753bc_286_0.png)

在编辑`/etc/inittab`文件之前，你应该知道此文件中的任何错误可能导致 Linux 无法启动到可以登录的程度。如果你无法登录，就无法使用系统。正如我接下来将解释的，在实际更改`/etc/inittab`文件中的默认运行级别之前，你可以尝试使用`init`命令尝试特定的运行级别。

## 使用 init 命令尝试新的运行级别

要运行新级别，不需要更改`/etc/inittab`文件中的默认运行级别。如果你以`root`身份登录，可以使用`init`命令更改运行级别（以及随之在 Linux 中运行的一组进程）。`init`命令的格式为：

```
init runlevel
```

在这里，`runlevel`必须是你想要的运行级别字符。例如，要将系统置于单用户模式，输入：

```
init 1
```

因此，如果你想尝试运行级别 5（假设你的系统尚未设置图形登录界面）而又不更改`/etc/inittab`文件，在 shell 提示符处输入：

```
init 5
```

系统应该结束所有当前进程并进入运行级别 5。默认情况下，`init`命令会在停止所有进程并启动运行级别 5 的新进程之前等待 20 秒。立即切换到运行级别 5，输入命令`init -t 5`。`-t`之后的数字表示`init`在切换级别之前等待的秒数。你也可以使用`telinit`命令，`init`的符号链接。如果你对`/etc/inittab`文件进行了更改并想重新加载配置，请使用`telinit`。

## 理解 Linux 启动

`init`在启动时运行许多脚本。注意`/etc/inittab`文件开头的几行：

- System initialization.
- `si::sysinit:/etc/rc.d/rc.sysinit`

正如第一行的注释所示，第二行导致`init`运行`/etc/rc.d/rc.sysinit`——Red Hat 启动脚本。`rc.sysinit`脚本执行许多任务，如挂载系统、设置时钟、配置键盘布局、启动网络以及加载许多驱动模块。`rc.sysinit`脚本通过调用其他脚本和读取`config`目录下的文件执行这些初始化任务。

在执行`/etc/rc.d/rc.sysinit`后，`init`进程带运行级别参数运行`/etc/rc.d/rc`。例如，对于运行级别 5，`/etc/inittab`中的下一行指定了`init`要执行：

```
15:5:wait:/etc/rc.d/rc 5
```

这表示`init`执行命令`/etc/rc.d/rc 5`并等待该命令完成。`/etc/rc.d/rc`脚本相当复杂。它的工作原理如下：它切换到与运行级别对应的目录。例如，切换到运行级别 5，脚本切换到`/etc/rc.d/rc5`。在与运行级别对应的目录中，它寻找所有以 `K` 开头的文件并带参数执行。这杀掉了运行中的进程。然后它找到所有以 `S` 开头的文件并带参数执行。这是指定运行级别所需的进程。要查看级别 5 发生了什么，输入以下命令：

```
ls /etc/rc.d/rc5
```

此命令提供了以下输出：

```
total 0
lrwxr-xr-x root root 15 Aug 16:24 K0ppoe ../init/ppoe
lrwxr-xr-x root root 14 Aug 16:08 K0innd ../init/innd
lrwxr-xr-x root root 13 Aug 19:22 K0nfs ../init/nfs
lrwxr-xr-x root root 16 Aug 16:24 K0rstart ../init/rstart
lrwxr-xr-x root root 17 Aug 16:14 K60rund ../init/usersd
lrwxr-xr-x root root 16 Aug 16:24 K61rwald ../init/rwald
lrwxr-xr-x root root 15 Aug 16:24 K65rhod ../init/rhod
lrwxr-xr-x root root 19 Aug 16:34 K63passwd ../init/passwd
lrwxr-xr-x root root 13 Aug 16:34 K35mb ../init/sm
lrwxr-xr-x root root 18 Aug 16:15 K54sparwitch ../init/sparwitch
lrwxr-xr-x root root 15 Aug 16:14 K51named ../init/named
lrwxr-xr-x root root 16 Aug 16:31 K50snmpd ../init/snmpd
lrwxr-xr-x root root 18 Aug 16:17 K60mars-new ../init/mars-new
lrwxr-xr-x root root 16 Aug 16:34 K64yserv ../init/yserv
lrwxr-xr-x root root 15 Aug 16:14 K50kudzu ../init/kudzu
lrwxr-xr-x root root 18 Aug 16:14 S11chains ../init/chains
lrwxr-xr-x root root 17 Aug 16:15 S10network ../init/network
lrwxr-xr-x root root 16 Aug 16:56 S12syslog ../init/syslog
lrwxr-xr-x root root 14 Aug 16:21 S13portmap ../init/portmap
lrwxr-xr-x root root 16 Aug 16:19 S14fslock ../init/fslock
lrwxr-xr-x root root 14 Aug 16:14 S15xdmap ../init/xdmap
```

如输出所示，所有以 `K` 和 `S` 开头的文件都是指向`/etc/rc.d`和`/etc/rc.d/init.d`目录中脚本的符号链接。事实上，`/etc/rc.d`脚本按照它们在目录列表中出现的顺序执行这些文件。

> 注意，目录列表中的最后一个文件是指向`rc.local`脚本的符号链接。这意味着`/etc/rc.d`会在所有其他脚本之后执行。你可以在 Linux 系统启动时，在该脚本中放置任何想要执行的命令。

![](img/448aa2bd6846782b632c764b035753bc_289_0.png)

大多数启动脚本位于`/etc/rc.d/init.d`目录。你可以手动调用该目录中的脚本来启动、停止或重启特定的进程。例如，要停止 Web 服务器，你输入以下命令：

```
/etc/rc.d/init.d/httpd stop
```

接后的响应显示：

```
Shuting down http: [ OK ]
```
