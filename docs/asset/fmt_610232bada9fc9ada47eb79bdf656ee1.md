
```text
[root@rh7 /etc]# more inittab
#
#  inittab   This file describes how the INIT process
#             should set up
#             the system in a certain run-level.
#
# Author:     Miquel van Smoorenburg,
#             <miquels@drinkel.nl.mugnet.org>
#             Modified for RHS Linux by Marc Ewing and
#             Donnie Barnes
#
#
# Default runlevel. The runlevels used by RHS are:
#   0 - halt (Do NOT set initdefault to this)
#   1 - Single user mode
#   2 - Multiuser, without NFS (The same as 3, if you do not
#       have networking)
#   3 - Full multiuser mode
#   4 - unused
#   5 - X11
#   6 - reboot (Do NOT set initdefault to this)
#
id:3:initdefault:
```

2. 如你所见，该系统默认设置为启动到运行级别 3。接下来，查看哪些服务被设置为在启动时启动。

```text
[root@rh7 rc3.d]# ls
K01ppppe    S08ipchains   S16apmd     S45spcminc  S80isdn     S95anacron
K20nfs      S10network    S20random   S55sshd     S80sendmail S97rhnsd
K20rawhd    S12syslog     S25netfs    S55rawdevices S85gpm    S991nuxconf
K45arpwatch S13portmap    S35ident    S60lpd      S90crond    S91local
S05kudzu    S14ntfslock   S40atd      S75keytable S90xfs
```

3. 如你所见，由于脚本 `S80sendmail` 位于 `/etc/rc3.d` 目录中，该服务将启动。（如果你的系统不启动 sendmail，请选择另一个脚本，例如 `gpm` 或 `crond`。）要确认该服务，你输入：`[root@rh7 rc3.d]# ps aux | grep sendmail`

```text
root         532   0.0   0.7  3232  336 ? S Mar14
0:01 sendmail: accepting connections
```

4. 要在下次启动时设置该服务不启动，你可以从目录中移除脚本链接，或者仅仅将其名称更改为不以 `S` 或 `K` 开头的名称。例如：

```text
[root@rh7 rc3.d]# mv S80sendmail H80sendlamail
```

5. 重启系统并确保该服务没有运行。

### 章节问题答案

#### 章节预测试

1. `init` 进程由内核启动，PID 为 1。

2. Sys V

3. `init`、`telinit`、`shutdown` 和 `halt`

4. `/etc/inittab`

5. `/etc/issue.net` 显示给网络登录用户。

6. 在 LILO 提示符处传递 `emergency` 启动参数。

7. 介质可能有问题，或者可能存在磁盘几何转换问题。

8. `ram=`

9. `/etc/lilo.conf`

10. 6

#### 评估问题

1. B. `restricted` 参数阻止控制台上的用户在不知晓预设密码的情况下发布启动参数。`password` 选项用于指定要输入的密码。其他选项无效。更多信息参见“配置 LILO”部分。

2. A. LILO 引导扇区应放置在驱动器的主引导记录中，而不是分区中。当安装了多个操作系统时，可以使用分区引导块。更多信息参见“使用 LILO”部分。

3. C. `root=` 参数告诉系统使用哪个卷作为根卷。设备名称应指向分区。不需要挂载点。更多信息参见“使用 LILO”部分。

4. A. 使用 `alias` 条目为你的引导映像提供第二个名称。`label` 条目为引导条目提供在 LILO 菜单上显示的名称。更多信息参见“配置 LILO”部分。

5. D. `telinit 5` 命令将系统更改为运行级别 5，在 Red Hat 中这是 GUI 模式。`startx` 命令用于从命令行启动 X Window 系统，但不用于启动时。`init 3` 命令会将系统更改为多用户文本模式。选项 B 无效。更多信息参见“使用运行级别”部分。

6. `shutdown -r now`。`-r` 选项指示系统重启，而 `now` 选项使系统立即执行。更多信息请参见“使用运行级别”章节。

7. `/sbin/halt`。更多信息请参见“使用运行级别”章节。

8. D. 其他条目无效。更多信息请参见“配置 `init` 进程”章节。

9. `/etc/issue.net`。本地用户将接收 `/etc/issue` 文件。更多信息请参见“自定义启动过程”章节。

10. A. `chkconfig` 工具从命令行使用，而 `ntsysv` 提供菜单界面。其他命令不提供运行级别信息。更多信息请参见“自定义启动过程”章节。

11. C. `-r` 参数更改感知到的根路径。它应指向根卷。更多信息请参见“排除 LILO 故障”章节。

12. `emergency`。`S` 参数仍然运行系统初始化脚本。更多信息请参见“引导至单用户模式”章节。

13. A. `--device` 参数指定软盘驱动器，编号从 0 开始。`mkboot` 工具不接受这些参数。更多信息请参见“创建启动盘”章节。

14. B. 某些 SCSI 磁盘需要 `linear` 选项。其他选项无效。更多信息请参见“配置 LILO”章节。

15. 6. 运行级别 0 停止系统，而运行级别 1 用于单用户模式。更多信息请参见“使用运行级别”章节。

16. A. `init` 进程是唯一具有运行级别 1 的进程。更多信息请参见“配置 `init` 进程”章节。

17. D. `once` 参数告知 `init` 只启动一次进程，不再重启。其他选项无效。更多信息请参见“配置 `init` 进程”章节。

18. B. BSD 风格的初始化使用少量大型脚本文件，而 Sys V 在目录层次结构中使用许多较小的文件。更多信息请参见“自定义启动过程”章节。

19. `inet_status`。可以查询 `/etc/init.d` 或 `/etc/rc.d/init.d` 中的 `inet_startup` 脚本以获取进程状态。更多信息请参见“Sys V 启动”章节。

20. A. LIL 错误由媒体故障或几何参数不匹配引起。LIL- 由损坏的描述符表引起。更多信息请参见“排除启动过程故障”章节。

#### 场景

1. 你可以将系统引导至单用户模式或紧急模式。找到启动挂起守护进程的脚本，对其进行故障排除或直接从该运行级别中移除。

2. 通过编辑 `/etc/inittab` 文件将系统更改为文本模式启动。要在不重启系统的情况下卸载 X 并切换到文本模式，可以执行 `telinit 3`。

3. 如果你已经制作了启动盘，可以使用这些盘启动系统。如果没有，你可以在其他 Linux 系统上创建启动盘，或从你的发行版网站下载启动和救援镜像。

### 使用 X

![](img/96d9ccd181675a8ae8b6a1146c919d2b_363_0.png)

### 考试目标

考试 102 ✦ 通用 Linux，第二部分

- 2.10 X
  - 安装与配置 XFree86。验证视频卡和显示器是否受 X 服务器支持，安装正确的 X 服务器，配置 X 服务器，安装 X 字体服务器，安装 X 所需的字体（可能需要手动编辑 `/etc/X11/XF86Config` 中的“文件”部分），根据视频卡和显示器自定义和调整 X。命令：`XF86Setup`、`xf86config`。文件：`/etc/X11/XF86Config`、`.xresources`。
  - 设置 XDM。开启和关闭 `xdm`，更改 `xdm` 问候语，更改 `xdm` 的默认位平面，配置 `xdm` 供 X-stations 使用。
