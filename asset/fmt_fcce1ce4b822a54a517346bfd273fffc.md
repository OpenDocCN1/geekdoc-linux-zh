
运行级别 2 到 5 留给发行版以及最终由你来定义。拥有这么多运行级别的想法是为了允许用户创建服务器可以进入的不同模式。传统上，许多 Linux 发行版会为图形桌面设置一个运行级别（在 Red Hat 中这是运行级别 5），并为无图形系统设置另一个运行级别（Red Hat 对此使用运行级别 3）。用户可以定义其他运行级别，例如启动一个无网络访问的系统。然后在启动时，你可以在启动提示符下传递一个参数，以用你选择的运行级别覆盖默认运行级别。系统启动后，你也可以使用 `init` 命令后跟运行级别来更改当前运行级别。因此，要在 Ubuntu 服务器系统上切换到单用户模式，你需要输入 `sudo init 1`。

### `init` Scripts

除了 `/etc/inittab` 之外，System V `init` 系统还有许多其他重要的文件和目录，用于组织所有主要服务的启动和关闭脚本，即 `init` 脚本。

- `/etc/init.d`: 该目录包含每个运行级别下每个服务的全部启动脚本。通常这些是标准的 shell 脚本，并且符合基本标准。每个脚本至少接受两个参数，start 和 stop，分别启动或停止一个服务（例如，你的 Web 服务器）。此外，`init` 脚本通常还接受一些额外选项，如 restart（停止后重新启动服务）、status（返回服务的当前状态）、reload（指示服务从其配置文件重新加载设置）以及 force-reload（强制服务重新加载其设置）。当你不带参数运行 `init` 脚本时，它通常应返回其接受的参数列表。

- `/etc/rc0.d` through `/etc/rc6.d`: 这些目录包含每个相应运行级别的 `init` 脚本。实际上，这些通常是对 `/etc/init.d` 下实际文件的符号链接。你会注意到的是，这些目录中的 `init` 脚本被赋予了特殊名称，以 S（start）、K（kill）或 D（disable）开头，然后跟一个数字。当 `init` 进入一个运行级别时，它会按数字顺序运行每个以 K 开头的脚本并传递 stop 参数，但仅当对应的 `init` 脚本在上一个运行级别中已启动时。然后 `init` 按数字顺序运行每个以 S 开头的脚本并传递 start 参数。任何以 D 开头的脚本，`init` 都会忽略——这允许你在特定运行级别中临时禁用一个脚本，或者你也可以直接删除符号链接。因此，如果你有两个脚本，`S01foo` 和 `S05bar`，`init` 在进入该特定运行级别时会先运行 `S01foo start`，然后运行 `S05bar start`。

- `/etc/rcS.d`: 在此目录中，你会找到 `init` 在更改到特定运行级别之前在启动时运行的所有系统 `init` 脚本。当你修改此目录中的脚本时要小心，因为如果它们卡住，可能会阻止你甚至进入单用户模式。

- `/etc/rc.local`: 并非每个发行版都使用 `rc.local`，但传统上这是为用户编辑而预留的 shell 脚本。它通常在 `init` 进程结束时执行，因此你可以将想要运行的额外脚本放在这里，而无需创建自己的 `init` 脚本。

所以这是一个标准 System V `init` 系统的示例启动过程。首先 `init` 启动并读取 `/etc/inittab` 以确定其默认运行级别，本例中该参数是运行级别 2。然后 `init` 转至 `/etc/rcS.d`，按数字顺序运行每个以 S 开头的脚本，并将 start 作为参数。随后 `init` 对 `/etc/rc2.d` 目录执行相同操作。最后 `init` 完成工作，但会留在后台运行，等待运行级别改变。

### Upstart

System V `init` 是一个优秀的系统，多年来在 Linux 上运行良好；然而，它也并非没有缺点。其一，`init` 脚本没有一种在服务终止时自动重新生成（respawn）的机制。因此，举例来说，如果 `cron` 守护进程因某种原因崩溃，你就必须另建工具来监控并重启该进程。

`init` 脚本的另一个问题是，它们通常只在运行级别改变或系统启动时才会执行；除此之外，除非你手动运行，否则不会被执行。依赖网络连接的 `init` 脚本就是一个很好的例子。在 Ubuntu 中，有一个名为 `networking` 的 `init` 脚本负责建立网络连接。所有依赖网络连接的 `init` 脚本都被赋予比该脚本更高的编号，以确保它们在 `networking` 脚本运行之后才执行。如果你从服务器上拔掉网线然后启动系统，会怎样？`networking` 脚本会运行，但所有需要网络连接的 `init` 脚本都会一个接一个地超时。最终你会看到登录提示并能够登录。登录之后，如果你插上网线并重启 `networking` 服务，你就能接上网络，但所有需要网络连接的服务都不会自动重启。你必须手动将它们一一启动。

Upstart 的设计不仅是为了解决 System V `init` 进程的部分缺陷，而且是为了提供一个更健壮的服务管理系统。Upstart 的一个主要特点是事件驱动。Upstart 持续监控系统以等待特定事件发生，一旦事件发生，Upstart 可被配置为针对这些事件采取相应动作。一些示例事件包括系统启动、系统关闭、按下 Ctrl-Alt-Del 组合键、运行级别改变，或者 Upstart 脚本启动或停止。为了了解事件驱动系统如何改进传统 `init` 脚本，让我们以之前那个在网线未插状态下启动的系统为例。你可以创建一个 Upstart 脚本，该脚本会被触发

接下来的几行导出一些环境变量，然后 `task` 选项告诉 `init` 这个脚本不会常驻——它会执行然后停止。

从 Upstart 脚本中实际运行的程序由 `script` 或 `exec` 选项来定义。对于 `exec` 选项，Upstart 会执行 `exec` 后面的命令及其所有参数，并跟踪其 PID。对于 `script` 选项，Upstart 会把后续各行当作一个 shell 脚本，直到遇到 `end script` 行为止。

尽管 Upstart 被设计为事件驱动，它仍然提供了检查 Upstart 作业状态以及按需启动/停止的方法。你可以使用名为 `status`、`start` 和 `stop` 的命令来检查状态、启动和停止 Upstart 脚本。Ubuntu 服务器上的一个 Upstart 作业是 `tty1` 作业，它会在 `tty1` 上启动 `getty` 程序。当管理员按下 Alt-F1 时，这给他/她提供了一个控制台。但是，假设出于某种原因你认为该控制台已挂起。下面是如何检查状态并重启该作业：

```text
$ sudo status tty1
tty1: start/running, process 789
$ sudo stop tty1
tty1 stop/waiting
$ sudo start tty1
tty1 start/running, process 2251
```

你还可以使用 `initctl list` 查询所有可用 Upstart 作业的状态：

```text
$ sudo initctl list
mountall-net stop/waiting
rc stop/waiting
rsyslog start/running, process 640
tty4 start/running, process 708
udev start/running, process 299
upstart-udev-bridge start/running, process 297
ureadahead-other stop/waiting
apport start/running
hwclock-save stop/waiting
irqbalance stop/waiting
```
