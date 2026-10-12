
# 不要直接将系统更改为运行级别 S

使用 `telinit` 请求系统更改到运行级别 1 时，系统会先进入运行级别 1，此时适当的系统进程（正在运行的系统服务）会被终止，然后自动进入运行级别 S。直接更改到运行级别 S 会将系统置于运行级别 S，但不会先终止任何进程；这通常是个坏主意。

Upstart `init` 守护程序仅在系统启动时参考 `/etc/inittab`（第 423 页）。此时没有来自之前运行级别的正在运行的进程，因此直接转到运行级别 S 不会有问题。

# 引导系统

*引导* 系统是将 Linux *内核*（第 1090 页）读取到系统内存中并启动运行的过程。有关系统启动初期步骤的更多信息，请参考第 551 页的“引导加载程序”。

在引导过程的最后一步，Linux 以 PID 号 1 运行 `init` 程序。`init` 程序是启动后运行的第一个真正的进程，也是所有系统进程的父进程。（这就是为什么当你以 `root` 身份运行并杀死进程 1 时，系统会崩溃的原因。）

`/etc/inittab` 文件（第 473 页）中的 `initdefault` 项告诉 `init` 将系统带到哪个运行级别（见表 11-1，第 424 页）。将 `initdefault` 设置为 3 可使系统在启动时显示文本登录消息；设置为 5 则显示图形登录屏幕（默认）。有关更多信息，请参见第 423 页的“rc-default 任务和 `inittab`”。

在引导过程的最后一步，Linux 以 PID 号 1 启动 `init` 守护程序（第 417 页）。`init` 守护程序是启动后运行的第一个真正的进程，也是所有系统进程的父进程。（这就是为什么当你以 `root` 权限杀死进程 1 时，系统会崩溃的原因。）

一旦 `init` 运行起来，`startup` 事件会触发 `rc5` 任务，该任务在系统进入任何运行级别时停止。`rc-default` 任务在 `rc5` 停止时启动。根据 `/etc/inittab`（第 423 页）的内容或缺少此文件，`rc-default` 要么

- 执行带有参数 S 的 `telinit`，这会触发 `rc5-sulogin` 并将系统带入恢复（单用户）模式，或者
- 执行带有参数 2 的 `telinit`，这会触发 `rc2`（第 422 页）并将系统带入多用户模式。

如果主引导记录（MBR）被覆盖，系统将无法引导进入 Linux，你需要重写 MBR。

# 初始化脚本：启动和停止系统服务

第一个运行的脚本是 `/etc/rc.d/rc.sysinit`，它执行基本的系统配置，包括设置系统时钟、主机名和键盘映射；设置交换分区；检查文件系统错误；以及开启配额管理（第 582 页）。此脚本由 `rc5` 任务运行（如 `/etc/event.d/rc5` 任务定义文件所指定；有关更多信息，请参见第 422 页）。

## 列出内核引导消息

若要保存内核引导消息的列表，请在系统启动并登录后立即运行 `dmesg`：

```
$ dmesg > dmesg.boot
```

此命令将内核消息保存到一个名为 `dmesg.boot` 的文件中。此列表可能具有教育意义；当你在引导过程中遇到问题时，它也可能很有用。有关更多信息，请参见第 553 页。

接下来，`rcn` 任务（参见第 422 页的“`rc2_task`”示例）运行 `/etc/rc.d/rcn` 初始化脚本，该脚本运行用于启动你首次启动系统时需要的服务的脚本，以及在系统从单用户模式切换到多用户模式再切回时需要启动或停止的服务的脚本。初始化（initialization）脚本，也称为 `rc`（run command）脚本，是位于 `/etc/rc.d/init.d` 目录中的 shell 脚本。它们通过 `/etc/rc.d/rcnd` 目录中的符号链接运行，其中 `n` 是系统正在进入的运行级别。

`/etc/rc.d/rcnd` 目录包含以字母 K 开头的脚本（例如，`K15httpd`、`K60nfs`、`K83bluetooth`）和以字母 `S` 开头的脚本（例如，`S25cups`、`S27NetworkManager`、`S55sshd`）。当进入新的运行级别时，每个 K（kill/终止）脚本都会以 `stop` 为参数执行，然后每个 S（start/启动）脚本都会以 `start` 为参数执行。每个 K 文件按数字顺序运行。S 文件以类似的方式运行。这种安排使得设置这些文件的人可以控制哪些服务被停止，哪些被启动，以及当系统进入特定运行级别时的顺序。使用带有 `start` 和 `stop` 参数的脚本增加了灵活性，因为它允许一个脚本根据调用时的参数来启动或终止进程。

要自定义系统初始化，你可以向 `/etc/rc.d/init.d` 目录添加 shell 脚本，并将这些文件的链接放置在 `/etc/rc.d/rcnd.d` 目录中。以下示例显示了几个指向 `cups` 脚本的链接。这些链接被调用来运行 `cups` 初始化脚本，以在不同的运行级别启动或停止 `cupsd` 守护程序：

```
$ pwd
/etc/rc.d
$ ls -1 */cups
-rwxr-xr-x. 1 root root 2947 Oct  8 04:45 init.d/cups
lrwxrwxrwx. 1 root root  14 Oct 14 20:38 rc0d/K10cups -> ../init.d/cups
-rwxrw-rwx. 1 root root  14 Oct 14 20:38 rc1.d/K10cups -> ../init.d/cups
-rwxrw-rwx. 1 root root  14 Oct 14 20:38 rc2.d/S25cups -> ../init.d/cups
-rwxrw-rwx. 1 root root  14 Oct 14 20:38 rc3.d/S25cups -> ../init.d/cups
-rwxrw-rwx. 1 root root  14 Oct 14 20:38 rc4.d/S25cups -> ../init.d/cups
-rwxrw-rwx. 1 root root  14 Oct 14 20:38 rc5.d/S25cups -> ../init.d/cups
-rwxrw-rwx. 1 root root  14 Oct 14 20:38 rc6.d/K10cups -> ../init.d/cups
```

`/etc/rc.d/rc*.d` 中的每个链接都应指向 `/etc/rc.d/init.d` 中的一个文件。例如，文件 `/etc/rc.d/rc1.d/K10cups` 是 `/etc/rc.d/init.d` 中名为 `cups` 文件的链接。（`/etc/rc.d/rc*.d` 目录中链接文件名的一部分数字可能会从一个操作系统版本变到下一个版本，但 `/etc/rc.d/init.d` 中的脚本始终具有相同的名称。）`/etc/rc.d/init.d` 目录中文件的名称具有功能性。因此，当你想要开启或关闭 NFS 服务时，使用 `nfs` 脚本。类似地，当你想要开启或关闭基本网络服务时，运行 `NetworkManager` 脚本。`cups` 脚本控制打印机守护程序。根据你想要执行的操作，每个脚本接受 `stop` 或 `start` 作为参数。一些脚本也接受其他参数，例如 `restart`、`reload` 和 `status`。不带参数运行脚本以显示用法消息，指示它接受哪些参数。

以下是调用初始化脚本的三个示例。你可能会发现使用 `service`（下一节讨论）来替代这些命令中的路径名更容易：

```
# /etc/rc.d/init.d/nfs stop
# /etc/rc.d/init.d/NetworkManager start
# /etc/rc.d/init.d/NetworkManager restart
```

第一个示例停止所有 NFS 进程（与通过网络提供文件系统相关的进程）。第二个示例启动与基本网络服务相关的所有进程。第三个示例停止这些相同的进程，然后重新启动它们。

# 维护 /etc/rc*.d 层次结构中的链接

> 提示 参见第 429 页，了解有关使用 `chkconfig` 维护 `/etc/rc*.d` 层次结构中符号链接的信息。

`/etc/rc.d/rc.local` 文件在其他初始化脚本之后执行。将用于自定义系统的命令放在 `rc.local` 中。虽然你可以向 `rc.local` 添加任何喜欢的命令，但最好在后台运行它们，这样即使它们挂起，也不会停止引导过程。

# service：配置服务 I

Fedora/RHEL 提供 `service`，这是一个方便的实用程序，可以报告或更改 `/etc/rc.d/init.d` 中任何系统服务的状态。替代上一节末尾描述的命令，你可以从任何目录给出以下命令：

```
# /sbin/service nfs stop
# /sbin/service NetworkManager start
# /sbin/service NetworkManager restart
```
