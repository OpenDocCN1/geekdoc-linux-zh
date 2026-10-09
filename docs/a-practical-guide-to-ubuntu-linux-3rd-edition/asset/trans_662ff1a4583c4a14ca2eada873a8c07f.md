
以下是启动并监控 tty1 上 getty 进程的服务（第 448 页）的作业定义文件：

```bash
$ cat /etc/init/tty1.conf
# tty1 - getty
#
# 此服务从系统启动到再次关机期间，始终在 tty1 上维护一个 getty 进程。

start on stopped rc RUNLEVEL=[2345]
stop on runlevel [!2345]

respawn
exec /sbin/getty -8 38400 tty1
```

start on 条目中的事件名为 **stopped**（参见 **stopped man** 页）。当 **rc** 任务停止且 **RUNLEVEL** 等于 2、3、4 或 5 时，此条目会启动 tty1 服务。由于 **rc** 任务在系统完成进入这些运行级别中的每一个时都会停止，因此 tty1 服务会在系统进入这些任何运行级别时启动。

**stop on** 条目中的事件名为 **runlevel**。当发出 **runlevel** 事件且参数不是 2、3、4 或 5 时，此条目会停止 tty1 服务——也就是说，当系统进入恢复模式、关机或重启时。

**respawn** 关键字告诉 init 在 tty1 服务终止时重新启动它。**exec** 条目在 tty1 上以 38,400 波特率运行一个无党派（-8）的 getty 进程。在下一个示例中，**initctl** 实用程序报告 **tty1** 服务已启动并正在作为进程 1061 运行；**ps** 报告了该进程的信息：

```bash
$ status tty1
tty1 start/running, process 1061
$ ps -ef | grep 1061
root     1061   1  0 12:26 tty1    00:00:00 /sbin/getty -8 38400 tty1
```

关于 **control-alt-delete** 任务的讨论请参见第 451 页，您可以使用它来关闭系统。

在 SysVinit 下，**/etc/inittab** 文件中的 **initdefault** 条目告诉 init 在系统启动时将其带到哪个运行级别（第 443 页）。Ubuntu 不包含 inittab 文件；相反，默认情况下，Upstart init 守护进程（使用 **rc-sysinit** 任务）将系统启动到多用户模式（运行级别 2）。如果您希望系统启动到不同的运行级别，请修改 rc-sysinit.conf 文件中的以下行：

```bash
$ cat /etc/init/rc-sysinit.conf
...
env DEFAULT_RUNLEVEL=2
...
```

### 请勿将系统设置为启动到运行级别 0 或 6

切勿将系统设置为启动到运行级别 0 或 6，否则系统将无法正常运行。若要启动到多用户模式（运行级别 2），请将 **DEFAULT_RUNLEVEL** 设置为 2。若要启动到恢复模式，请将 **DEFAULT_RUNLEVEL** 设置为 5。

将 `DEFAULT_RUNLEVEL` 的值从 2 更改为 5 会导致系统启动到恢复模式（运行级别 5；请参见第 444 页的警告）。当系统以恢复模式启动时，如果系统上的 **root** 账户未锁定（第 431 页），`init` 在显示 **root** 提示符之前会请求 **root** 密码。否则，它将直接显示 **root** 提示符，而不请求密码。

## SysVinit (rc) 脚本：启动和停止系统服务

- **rc 脚本**：init（初始化）脚本也称为 **rc**（运行命令）脚本，是位于 `/etc/init.d` 目录中的 shell 脚本。它们通过 `/etc/rcn.d` 目录中的符号链接运行，其中 *n* 是系统正在进入的运行级别。

> 如第 434 页所述，Ubuntu 使用 Upstart 模拟运行级别，以辅助迁移并提供与其他发行版软件的兼容性。本节解释了 `init` 脚本如何与（模拟的）运行级别配合工作以控制系统服务。本节中描述的 /etc/rcn.d 和 /etc/init.d 目录中的许多脚本建议您使用相应的 `initctl` 命令来替代脚本，因为这些目录中的链接已被 `/etc/init`（第 434 页）中的作业控制文件所取代。

`/etc/rcn.d` 目录中包含名称以 K 开头的脚本（如 K19`cupsys`、K20`dhcp`、K74`bluetooth` 等）和名称以 S 开头的脚本（如 S15`bind9`、S18`is`、S20`exim4` 等）。当进入新的运行级别时，每个 K（kill）脚本都会以 `stop` 参数执行，然后每个 S（start）脚本都会以 `start` 参数执行。每个 K 文件按数字顺序运行。S 文件也以类似方式运行。这种安排允许设置这些文件的人控制系统何时进入特定运行级别时停止哪些服务、启动哪些服务以及顺序。使用带有 **start** 和 **stop** 参数的脚本可以提高灵活性，因为它允许根据调用的参数，由同一个脚本既启动又终止进程。

若要自定义系统初始化，您可以向 `/etc/init.d` 目录添加 shell 脚本，并在 `/etc/rcn.d` 目录中放置指向这些文件的链接（尽管在实践中最好使用 `sysv-rc-conf` [下文将讨论] 来创建链接）。

以下示例显示了几个指向 `cupsys` init 脚本的链接。这些链接用于在各个运行级别调用 `cupsys` init 脚本，以启动或停止 `cupsys` 守护进程：

```bash
$ ls -l /etc/rc*/s*cupsys*
lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc1.d/K80cupsys -> ../init.d/cupsys
lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc2.d/S50cupsys -> ../init.d/cupsys
lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc3.d/S50cupsys -> ../init.d/cupsys
lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc4.d/S50cupsys -> ../init.d/cupsys
lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc5.d/S50cupsys -> ../init.d/cupsys
```

`/etc/rcn.d` 中的每个链接都指向 `/etc/init.d` 中的一个文件。例如，文件 `/etc/rc2.d/S50cupsys` 是 `/etc/init.d` 中名为 `cupsys` 文件的链接。（`/etc/rcn.d` 目录中链接文件名中的数字可能会随 Ubuntu 的一个版本到下一个版本而变化，但 `/etc/init.d` 中的脚本始终具有相同的名称。）

init.d 目录中文件的名称具有功能性。因此，当您想要开启或关闭 NFS 服务时，请使用 nfs-kernel-server 脚本。同样，当您想要开启或关闭基本网络服务时，请运行 networking 脚本。cups 脚本控制打印机守护进程。根据您要执行的操作，每个脚本接受 stop 或 start 参数。一些脚本也接受其他参数，如 restart、reload 和 status。在不带参数的情况下运行脚本将显示一条用法消息，指示其接受哪些参数。

以下是调用 init 脚本的三个示例。您可能会发现使用下一节讨论的 service 来替代这些命令中的路径名会更简单：

```bash
$ sudo /etc/init.d/nfs-kernel-server stop
$ sudo /etc/init.d/networking start
$ sudo /etc/init.d/networking restart
```

第一个示例停止所有 NFS 服务器进程（与通过网络提供文件系统相关的进程）。第二个示例启动所有与基本网络服务相关的进程。第三个示例停止这些相同的进程，然后重新启动它们。

/etc/rc.local 文件在系统启动时，在其他 init 脚本执行之后运行。将用于定制系统的命令放入 rc.local。虽然您可以向 rc.local 添加任何您喜欢的命令，但最好在后台运行它们；这样，即使它们挂起，也不会阻止启动过程。

## Service：配置服务 I

Ubuntu 提供了 `service`，这是一个便捷的实用程序，可以报告或更改 /etc/init（第 435 页）中任何作业以及 /etc/init.d（第 440 页）中任何系统服务的状态。Ubuntu 引入了此实用程序以兼容 Fedora/RHEL 的 `service` 实用程序。使用任意目录中的以下命令，即可替代前一部分末尾描述的命令：

```bash
$ sudo service nfs-kernel-server stop
$ sudo service networking start
$ sudo service networking restart
```

命令 `service --status-all` 显示所有系统服务的状态。下一节将探索配置系统服务的另一种方式。

## Sysv-rc-conf：配置服务 II

`sysv-rc-conf` 实用程序（sysv-rc-conf 包）使系统管理员更容易维护 `/etc/init.d` 目录层级。此实用程序可以添加、删除和列出系统服务的启动信息。您可能还希望尝试图形化启动管理器 `bum`（bum 包），本书未涵盖此工具。

您可以以伪图形或文本模式运行 `sysv-rc-conf`。在伪图形模式下，当您输入更改时，它会更改配置文件，并且还可以启动和停止服务。有关此模式的更多信息，请参见 `sysv-rc-conf` 的 man 页，或不带任何参数运行 `sysv-rc-conf` 并输入命令 `h`。本节讨论以文本模式使用 `sysv-rc-conf`，在此模式下它会更改配置

