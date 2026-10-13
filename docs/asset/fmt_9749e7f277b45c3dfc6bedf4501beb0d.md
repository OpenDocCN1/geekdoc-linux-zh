
你还可以使用 `telinit` 命令，它只是一个指向 `init` 的符号链接（快捷方式）。如果你修改了 `/etc/inittab` 文件并希望 `init` 重新加载其配置文件，请使用命令 `telinit q`。

### 理解 Fedora Core 启动脚本

`init` 进程在系统启动时运行多个脚本。如果你查看 `/etc/inittab` 文件，你会发现文件开头附近有如下行：

```text
#### System initialization.
si::sysinit:/etc/rc.d/rc.sysinit
```

第一行是注释行。第二行使 `init` 运行 `/etc/rc.d/rc.sysinit` 脚本——这是 `init` 运行的第一个 Fedora Core 启动脚本。`rc.sysinit` 脚本执行许多初始化任务，例如挂载文件系统、设置时钟、配置键盘布局、启动网络以及加载许多其他驱动程序模块。`rc.sysinit` 脚本通过调用许多其他脚本并读取位于 `/etc/sysconfig` 目录中的配置文件来执行这些初始化任务。

执行完 `/etc/rc.d/rc.sysinit` 脚本后，`init` 进程将运行带有运行级别作为参数的 `/etc/rc.d/rc` 脚本。例如，对于运行级别 5，`/etc/inittab` 中的以下行指定了 `init` 执行的命令：

```text
15:5:wait:/etc/rc.d/rc 5
```

这个示例说明 `init` 执行命令 `/etc/rc.d/rc 5` 并等待该命令完成。

`/etc/rc.d/rc` 脚本有些复杂。以下是其工作原理：

- 它切换到对应运行级别的目录。例如，要切换到运行级别 5，脚本会切换到 `/etc/rc.d/rc5.d` 目录。
- 在对应运行级别的目录中，`/etc/rc.d/rc` 查找所有以 `K` 开头的文件，并使用 `stop` 参数执行它们。此参数会终止当前正在运行的进程。然后，它查找所有以 `S` 开头的文件，并使用 `start` 参数执行每个文件。此参数会启动指定运行级别所需的进程。

要查看在运行级别 5 下执行的内容，请输入以下命令：

`ls -l /etc/rc.d/rc5.d`

在生成的列表中，K 脚本——即文件名以 K 开头的文件——停止（或“杀死”）服务器，而 S 脚本启动服务器。`/etc/rc.d/rc` 脚本严格按照文件在目录列表中出现的顺序执行这些文件。

名为 `/etc/rc.d/rc.local` 的脚本在所有其他脚本之后执行。因此，你可以在该脚本中放置任何你希望在 Fedora Core 系统启动时执行的命令。

![](img/9f89727199836b0f871f1745838aa8b2_428_0.png)

#### 手动启动和停止服务器

大多数服务器启动脚本位于 `/etc/init.d` 目录中（脚本实际上位于 `/etc/rc.d/init.d`，但 `/etc/init.d` 是 `/etc/rc.d/init.d` 的快捷方式）。你可以手动调用此目录中的脚本来启动、停止或重启特定进程——通常是服务器。例如，要停止 Web 服务器（服务器程序名为 `httpd`），请输入以下命令：

`/etc/rc.d/init.d/httpd stop`

如果 `httpd` 正在运行且你想重启它，请输入以下命令：

`/etc/init.d/httpd restart`

通过熟悉 `/etc/init.d` 目录中的脚本，你可以提升系统管理技能。要查看其列表，请输入以下命令：

`ls /etc/init.d`

例如，以下是我系统中典型的脚本列表：

| aprld | dovecot | killall | nfslock | rpcgssd | syslog |
|:---|:---|:---|:---|:---|:---|

| aep1000 | firstboot | kudzu | nscd | rpcbind | tux |
| anacron | functions | mdmonitor | ntpd | rpcsvcs | vncserver |
| apmd | gpm | mdmimpd | pcmcia | saslauthd | vsftpd |
| atd | halt | messaged | portmap | sendmail | winbind |
| autofs | httpd | microcode_ctl | postgresql | simple | xfs |
| bcm5820 | innnd | named | psacct | smartd | xinetd |
| cpuspeed | iptables | netdump | random | smbd | ypbind |
| crond | irda | netfs | randevides | snd | yppasswd |
| cups | irqbalance | netplug | readahead | snmptrap | ypserv |
| dc_client | isdn | network | readahead | squid | ypxfrd |
| dc_server | kdirate | nfs | readahead_early | sshd | yum |

脚本名称会让你对脚本可以启动和停止哪些服务器有所线索。例如，`nfs` 脚本启动和停止 NFS（Network File System，网络文件系统）服务所需的进程。当你有时间时，你可以研究其中一些脚本，以了解每个脚本的作用。你不需要理解所有的 shell 编程；注释有助于你了解每个脚本的目的。

![](img/9f89727199836b0f871f1745838aa8b2_429_0.png)

使用 `service` 命令作为快捷方式，运行 `/etc/init.d` 中用于启动、停止或重启服务器的脚本。例如，要启动 Web 服务器，请输入此命令：

```
service httpd start
```

要重启该服务器，请输入以下命令：

```
service httpd restart
```

### 在系统启动时自动启动服务器

你希望某些服务器每次启动系统时都自动启动。例如，如果你运行 Web 服务器，你希望在系统启动时 `httpd` 服务器也能启动。你可以通过使用 `chkconfig` 命令来实现这一点。例如，要设置 `httpd` 在系统进入运行级别 3、4 或 5 时启动，请输入以下命令（以 root 身份登录时）：

```
chkconfig --level 345 httpd on
```

你还可以使用 `chkconfig` 命令来检查哪些服务器已开启或关闭。例如，要查看所有运行级别的所有服务器完整列表，请输入以下命令：

```
chkconfig --list
```

如果你想查看单个服务器（如 `httpd`）的状态，将该服务器的名称添加到 `chkconfig` 命令中，如下所示：

### 理解 GUI 启动

图形登录界面在运行级别 5 下启动。当 `init` 进程在运行级别 5 下启动系统时，`/etc/inittab` 文件的最后一行使 `init` 启动图形登录过程。以下是 `/etc/inittab` 文件最后一行的样子（数字 5 表示运行级别 5）：

```
x:5:respawn:/etc/X11/prefdm -nodamemo
```
