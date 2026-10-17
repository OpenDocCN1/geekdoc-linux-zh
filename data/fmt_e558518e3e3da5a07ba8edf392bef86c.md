
# 主资源配置脚本

进入`/etc/rc`是一个完全自动化的“框架”，它读取全局配置文件，然后按特定顺序执行`/etc/rc.d`中的一系列其他脚本。现在你知道了`/etc/rc.d`脚本的作用，我们可以看看如何配置`/etc/rc`的行为。

## `/etc/defaults/rc.conf`文件

`/etc/rc`程序是一个`shell`脚本，其操作基于数十个不同变量的状态。如果某个变量（例如`sendmail_enable`）设置为`YES`，`/etc/rc`将运行启动`Sendmail`的`/etc/rc.d`脚本。如果变量设置为`NO`，则不运行`Sendmail`脚本。

`FreeBSD`安装时带有一个文件，定义了对`/etc/rc`有意义的所有变量的所有默认状态。该文件是`/etc/defaults/rc.conf`。`/etc/rc`的第一件事就是读取此文件，以便知道对所有配置变量使用什么默认假设。

让我们看看`/etc/defaults/rc.conf`中的一个典型块，如列表 7.1 所示。

### 列表 7.1 `/etc/defaults/rc.conf`摘录

```
# named. It may be possible to run named in a sandbox, man security for
# details.
#
named_enable="NO"      # Run named, the DNS server (or NO).
named_program="named"  # path to named, if you want a different one.
named_flags=""         # Flags for named
#named_flags="-u bind -g bind"  # Flags for named
```

通过查看`/etc/defaults/rc.conf`，你可以找到`/etc/rc`在你明确覆盖之前会做什么。在这种情况下，你可以看到默认行为是不运行`named`。

## `/etc/rc.conf`文件

如何覆盖`/etc/defaults/rc.conf`中的默认设置？你使用`/etc/rc.conf`来实现，它在`/etc/rc`读取默认值后立即被读入。`FreeBSD`即使完全没有`/etc/rc.conf`文件也能正常运行；它只是一个纯文本文件，你可以用文本编辑器手动创建，每行一个变量。你只需向此文件添加想要覆盖的变量，以便使用你期望的值而不是默认值。使用`sysinstall`进行配置更改后，与这些更改相关的某些变量会由该程序自动写入`/etc/rc.conf`。你可以使用`more /etc/rc.conf`查看其中的内容。

假设我们确实想运行`named`。在最简单的情况下，我们所要做的就是编辑`/etc/rc.conf`（覆盖文件），并在文件中的任何位置添加以下行：

```
named_enable="YES"
```

`/etc/defaults/rc.conf`中其余的`named_*`变量无需复制到覆盖文件中；记住，`defaults`文件中的每个变量都由`init`加载到内存中，只有在该块的“主开关”被切换到“YES”时才重要。如果是这样，这些变量将在`/etc/rc`中的执行循环中使用，以启动我们正在处理的块所控制的进程（在本例中为`named`）。

你也可以使用这些其他变量进行微调，并且可以同样轻松地覆盖它们。假设你的域名服务器程序是一个名为`mynamed`的定制版本。假设你还创建了一个`bind`用户和组，意图让域名服务器以该用户和组运行，这样它就不会那么容易受到安全攻击。好吧，要处理这个问题，你需要做的全部就是（假设`mynamed`的行为和命令行选项与`named`相同）向`/etc/rc.conf`添加这两行：

```
named_program="mynamed"
named_flags="-u bind -g bind"
```

从现在开始，当你启动系统并在控制台消息中看到`Doing additional network setup:`之后出现`named`时，你就知道它正在将你的覆盖设置应用到默认值之上并自动运行域名服务器。

出现在`/etc/rc.conf`中最典型的变量是`TCP/IP`配置参数，因为它们对于每个系统来说自然会不同；毕竟`FreeBSD`不能很好地在默认值中指定它们。清单 7.2 显示了新安装`FreeBSD`后典型的`/etc/rc.conf`。

### LISTING 7.2 新安装的 `/etc/rc.conf`

```
# This file now contains just the overrides from /etc/defaults/rc.conf
# please make all changes to this file.

# Enable network daemons for user convenience.
# -- sysinstall generated deltas -- #
kern_securelevel="1"
kern_securelevel_enable="YES"
linux_enable="YES"
sendmail_enable="YES"
sshd_enable="YES"
portmap_enable="NO"
nfs_server_enable="NO"
inetd_enable="NO"
network_interfaces="fxp0 lo0"
ifconfig_fxp0="inet 10.6.7.101 netmask 255.0.0.0"
defaultrouter="10.6.1.1"
hostname="freebsd1.testnetwork.com"
usbd_enable="YES"
```

其中一些变量实际上与`defaults`文件重复；尽管如此，将它们也放在覆盖文件中仍然是有用的，因为其中许多功能（例如`NFS`服务器）现在都有一种一键切换控制。

> 如果你向`/etc/rc.conf`添加一个变量，请确保该变量的另一个版本不在文件中——至少确保它不会出现在文件后面的位置。变量是按顺序读取的，覆盖的工作方式很简单：系统看到的每个变量的最后一次出现就是它使用的那一次。如果你总是小心只在`rc.conf`的末尾添加变量，应该就没问题。

许多程序在安装时必须为自己在启动时启动安装一种方式；`/etc/rc.conf`然而不是它们的地方。该文件`supposed`只由你、管理员以及`sysinstall`程序在对核心系统进行更改时触碰。对于用户安装的程序（`ports`和`packages`）以及`/etc/rc`和朋友们不知道的任何脚本，它们的启动脚本和配置文件有另一种结构：`/usr/local/etc`层级。

## `/usr/local/etc`和`/usr/local/X11R6/etc`目录

你自己安装的程序被认为是本地的，意味着它们仅适用于你的特定机器而不是`FreeBSD`本身。本地安装程序的配置文件进入`FreeBSD`中的`/usr/local`层级作为其结构约定之一。有一个`/usr/local/etc/rc.d`目录，其操作等同于`/etc/rc.d`——除了因为其中的文件适用于你安装的程序，而不是核心系统，你可以自己编辑这些文件以更改这些程序的行为。

`init`在运行完所有其他`/etc/rc.d`脚本后才会将注意力转向`/usr/local/etc/rc.d`。目录中以`.sh`结尾的任何可执行文件都将按字典顺序执行。将安装在此处的示例文件包括`apache.sh`、`mysql-server.sh`和`samba.sh`。这些脚本是`ports`或`packages`的一部分定制构建的（参见 Hour 6，“Adding and Removing Third-Party Software”，了解有关`ports`和`packages`的更多信息），并且每个脚本都针对接受`start`或`stop`参数进行了调整。当`init`运行每个脚本时，它使用`start`参数。请注意，你可以在运行时同样轻松地自己运行这些脚本——例如，在不重新启动的情况下启动新安装的服务，

```
# /usr/local/etc/rc.d/apache.sh start
```

一些`ports`或`packages`将以`.sample`的次要后缀安装（例如`samba.sh.sample`），因为它所属的程序必须在成功运行之前正确配置。例如，`Apache`在安装后无需对配置文件进行任何进一步修改即可立即运行（尽管你无疑也会修改它们），因此它安装了一个`apache.sh`文件，如果你立即重新启动它，该文件可以干净地运行程序。但`Samba`（我们将在 Hour 24，“File Sharing”中讨论）必须先进行调整才能在你的机器上运行；如果你在安装后立即运行脚本，它将无法启动守护进程。你需要在`init`在启动时运行它之前重命名脚本以删除`.sample`扩展名。
