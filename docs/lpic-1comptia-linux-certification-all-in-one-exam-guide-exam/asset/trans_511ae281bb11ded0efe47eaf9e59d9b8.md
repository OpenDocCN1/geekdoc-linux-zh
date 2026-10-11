

终止或启动脚本文件名中的编号在此时起作用。该编号决定了脚本运行的顺序。这确保了其他服务所依赖的服务会首先启动。例如，被分配编号为 01 的脚本将在被分配编号为 02 的脚本之前运行。这意味着，位于 rc5.d 目录中的 `S02network` 文件将在 `S01dbus` 之后运行，但在 `S03syslog` 之前运行。

为了阐明这一点，让我们通过一个示例来进行说明。假设你需要将系统从运行级别 3 切换到运行级别 5。以下是发生的过程：

- 1. 你在 shell 提示符下输入 `init 3`（作为 root 用户）。
- 2. init 进程检查 `/etc/inittab` 配置文件，该文件通常指定运行 `/etc/init.d` 目录下的 `rc` 脚本，并指示其将系统切换到运行级别 5。
- 3. rc 进程在当前运行级别目录中运行终止脚本，以关闭在新运行级别中应被禁用的正在运行的服务。
- 4. rc 进程在新运行级别目录中运行启动脚本，以启动当前未运行但在新运行级别中应运行的服务。

> **注意** 如果你在 shell 提示符下输入 `init 0` 或 `init 6`，系统将停止（`init 0`）或重启（`init 6`）。你还可以使用 `telinit` 命令代替 `init` 来更改运行级别。功能和语法是相同的。

你还可以通过让引导加载程序将所需的运行级别作为内核选项发送给 Linux 内核，在系统启动时更改运行级别。例如，在 openSUSE 系统上，你只需在 GRUB 引导菜单的 Boot Options（启动选项）字段中，将想要启动进入的运行级别作为最后一个参数添加即可。例如，在图 6-18 中，数字 3 被添加为最后一个启动选项。这个数字会被传递给 init 进程，并告知 init 启动到哪个运行级别。

接下来，让我们回顾一下将服务配置为在特定运行级别运行的流程。

## 配置服务在指定运行级别默认运行

如果你希望配置系统服务在启动时自动运行，你必须将其与系统运行级别关联，并指定该服务是关闭还是开启。

每当安装一个守护进程（daemon）时，无论是在系统安装过程中还是通过 rpm 工具，init 脚本都会被复制到你的 init 目录（`/etc/init.d` 或 `/etc/rc.d/init.d`）中。你可以使用 `insserv` 或 `chkconfig` 命令来配置每个 init 脚本关联的运行级别。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_255_0.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_255_1.png)

`insserv` 命令读取 init 脚本中 INIT INFO 块的信息，以确定关联的服务默认应在哪些运行级别中运行。openSUSE 系统中 ntp init 脚本的 INIT INFO 块如本例所示：

```
### BEGIN INIT INFO
# Provides:      ntp ntpd xntpd
# Required-Start: $remote_fs $syslog $named
# Required-Stop:  $remote_fs $syslog
# Should-Start: network-remoteofs
# Should-Stop: network-remoteofs
# Default-Start:  3 5
# Default-Stop:   0 1 2 6
# Short-Description: Network time protocol daemon (ntpd)
# Description:     Start network time protocol daemon (NTPD).
### END INIT INFO
```

正如你在本例中看到的，INIT INFO 块为给定的 Linux 守护进程提供了几个关键信息：

- init 脚本管理的服务（Provides）
- 在此服务启动前必须启动的服务（Required-Start）
- 守护进程应默认运行的运行级别（Default-Start）
- 守护进程不应默认运行的运行级别（Default-Stop）

Default-Start 和 Default-Stop 参数被 `insserv` 命令用于确定应在哪些运行级别目录中创建相应的启动和终止脚本链接。使用前例中显示的 INIT INFO 块，`insserv` 命令将在 rc3.d 和 rc5.d 目录中创建启动脚本链接，同时在 rc1.d 和 rc2.d 目录中创建终止脚本链接。

使用 `insserv` 的语法是 `insserv service_name`。该命令会在服务 init 脚本的 INIT INFO 块中 Default-Start 指令所列的运行级别上启用指定的守护进程。它还会在 INIT INFO 块中 Default-Stop 指令所列的运行级别上禁用该守护进程。

`insserv` 工具还可以用于禁用服务（从而移除各种 rcx.d 目录中该服务的所有链接），并在其当前正在运行时停止该服务。执行此操作的语法是 `insserv -r service_name`。

如果某个服务已经被启用，而你希望更改其默认运行级别，可以使用 `insserv` 来实现更改。请执行以下操作：

- 1. 在你的 init 脚本目录中打开相应的 init 脚本，并编辑 INIT INFO 块中的 Default-Start 和 Default-Stop 参数。
- 2. 保存你对文件的更改。
- 3. 在 shell 提示符下输入 `insserv -d service_name`。

执行此操作时，`insserv` 命令会在各种 rcx.d 目录中重新创建相应的启动和终止脚本链接。

你也可以使用 `insserv` 启用守护进程，但完全忽略其 init 脚本中的 Default-Start 和 Default-Stop 参数。要做到这一点，请采取以下步骤：

- 1. 如果该守护进程已在默认运行级别上启用，请在 shell 提示符下输入 `insserv -r service_name` 以移除所有启动和终止脚本链接。
- 2. 通过输入 `insserv service_name,start=comma-separated_list_of_runlevels` 创建新的自定义启动和终止脚本链接。例如，`insserv ntp,start=3,5`。

除了 `insserv`，你还可以使用 `chkconfig` 命令来管理守护进程的运行级别。如果你想查看服务的当前运行级别配置，请在 shell 提示符下输入 `chkconfig -l daemon_name`。你还可以输入 `chkconfig -l` 来查看系统上安装的所有守护进程的状态。在下面的示例中，使用 `chkconfig` 命令查看 ntp 守护进程的运行级别配置。

```
ws1:/etc/init.d # chkconfig -l ntp
ntp                     0:off 1:off 2:off 3:off 4:off 5:off 6:off
ws1:/etc/init.d #
```

如你在此处所见，ntp 服务未配置为在任何运行级别启动。如果你希望配置守护进程在其默认运行级别启动，你可以输入 `chkconfig daemon_name on`。你也可以使用 `chkconfig` 命令精确指定希望守护进程在哪些级别启动。例如，假设我们希望 ntp 守护进程在运行级别 3 和 5 中运行。我们可以通过输入 `chkconfig -s ntp 35` 来实现这一点。这指定了 ntp 服务（由 -s 选项指定）在运行级别 3 和 5 上启用。显示如下：

```
ws1:/etc/init.d # chkconfig -s ntp 35
ws1:/etc/init.d # chkconfig -l ntp
ntp                     0:off 1:off 2:off 3:on  4:off 5:on  6:off
ws1:/etc/init.d #
```

要禁用服务，请输入 `chkconfig service_name off`。例如，要禁用之前启用的 ntp 服务，你会输入 `chkconfig ntp off`：

```
ws1:/etc/init.d # chkconfig ntp off
ws1:/etc/init.d # chkconfig -l ntp
ntp                     0:off 1:off 2:off 3:off 4:off 5:off 6:off
ws1:/etc/init.d #
```

你还可以通过简单地输入 `chkconfig -l` 来使用 `chkconfig` 查看系统上安装的所有服务的运行级别配置，如下所示：

```
ws1:/etc/init.d # chkconfig -l
SUBFirewall12_init      0:off 1:off 2:off 3:on  4:on  5:on  6:off
SUBFirewall12_setup     0:off 1:off 2:off 3:on  4:on  5:on  6:off
aeventd                 0:off 1:off 2:off 3:off 4:off 5:off 6:off
acpid                   0:off 1:off 2:on  3:on  4:off 5:on  6:off
alsa sound              0:off 1:off 2:on  3:on  4:off 5:on  6:off
atd                     0:off 1:off 2:off 3:off 4:off 5:off 6:off
auditd                  0:off 1:off 2:off 3:on  4:off 5:on  6:off
autofs                  0:off 1:off 2:off 3:off 4:off 5:off 6:off
...
```

让我们在下方的练习中练习操作 Linux 运行级别。

## 练习 6-2：操作 Linux 运行级别

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_258_0.png)

**视频** 要了解更多信息，请观看 *Exercise 6-2*。

在这个练习中，你将练习在你的 Linux 系统上操作运行级别。请完成以下操作：

- 1. 启动你的 Linux 系统并以标准用户身份登录。
- 2. 打开一个终端会话。
- 3. 通过输入 `su –` 后跟你的 root 用户密码，切换到你的 root 用户账户。
- 4. 通过执行以下操作，练习从 shell 提示符更改当前运行级别：
    - a. 在 shell 提示符下输入 `runlevel` 查看当前运行级别。显示的第一个数字表示你系统之前的运行级别；第二个数字表示你系统当前的运行级别。
        - 如果你安装的是图形化系统，当前运行级别应为 5。如果你安装的是基于文本的系统，当前运行级别应为 3。如果你的第一个运行级别参数显示为 *N*，这意味着系统从未处于当前运行级别以外的其他运行级别。
    - b. 在 shell 提示符下输入 `init 3` 切换到运行级别 3。
    - c. 在提示时，以 root 用户身份登录。
    - d. 在 shell 提示符下输入 `init 5` 切换回运行级别 5。
    - e. 重新登录系统。
- 5. 通过执行以下操作，将默认运行级别更改为 3：
    - a. 打开一个终端会话。
    - b. 在 shell 提示符下，使用 `su –` 命令切换到 root 用户账户。
    - c. 在 shell 提示符下，输入 `vi /etc/inittab`。
    - d. 向下滚动到写着 `id:5:initdefault:` 的行。
    - e. 按 `INSERT` 键。
    - f. 将此行的数字 5 更改为 3。
    - g. 按 `ESC`，然后输入 `exit`。
    - h. 在 shell 提示符下输入 `init 6` 重启系统。
        - 你的系统应启动到基于文本的登录 shell。
    - i. 以 root 用户身份登录。

