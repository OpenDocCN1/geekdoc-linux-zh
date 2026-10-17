
# `/etc/rc.d`

`init.d` `rc0.d` `rc2.d` `rc4.d` `rc6.d`

`rc` `rc1.d` `rc3.d` `rc5.d` `rclocal`

假设值为 5，`rc` 脚本执行 `/etc/rc.d/rc5` 目录下的所有脚本并启动图形登录。例如，如果 Fedora 启动到运行级别 5，以字母 K 开头并在 `/etc/rc.d/rc5` 开头的脚本将被执行：

```
# /etc/rc.d/rc5

K0lyum K20bootparam K28amd K45named K61ldap

K74pyxfrd S05kudzu S24pcmcia S85gpm K05innod

K20iscci S05sendmail K46radvad K65ident K44bagged

s08iptables S25netfs S90around S05laslauth K20netump-server

K34dhrelay K50netump K65kadmin K84sp6fd S08ipchains

S26amd S90FreeWnn K10psactct K34passwd

K12canna K20users S35dhcpcd K50utux K68krb5kdc
```

## 启动时运行服务

这些脚本实际上是 `/etc/rc.d/init.d/` 下服务脚本的符号链接，其外观可能取决于你运行的是工作站还是服务器安装版本，以及系统上安装了哪些服务或软件包包：

```bash
# ls /etc/rc.d/init.d/

acpid bpgpd firstboot iptables keytable mars-new nfs

postscript ripld smartd vncserver zebra aep1000 bluetooth

FreeWnn ipchains killall mdnmonitor nfslock pricey

ripngd smb vsptpd and bootparamd functions iptions

kpop messagebox ns-ps-acat routed snmpd winbind

anron canna gkrellnd irda krbs524 microcode_ctl nptd

rpx restart smnptrap xfs cpyqqard gpm

irqbalance krbs5kdc mysql radius usersd

spassassin xinetd apache crowd halt issci kudzu

named ospfd radvd rwalld squid ybind

random sshd ypppasswd add dhcpd

http isicom lisa netdum-server pcmia raarpd

lasauthd syslog ypsvers autohley ident kadmin

l_sensors netfs portmap wavdevices itself

nnpyfrd bcm5820 docot indeed mailman

network postfix rhns single ups yum
```

`rc5.d` 链接以字母和数字开头，例如 `K15` 或 `S10`。这些前缀中的 `(K)` 或 `(S)` 表示特定服务应该被杀死 `(K)` 还是启动 `(S)`，并向特定的 `/etc/rc.d/init.d/` 脚本传递 `stop` 或 `start` 值。前缀中的数字用于按特定顺序执行脚本。符号链接必须界定它们启动的顺序。特定的数字并没有绝对之分，但某些服务需要在其他服务之前运行。例如，你不会希望你的 Fedora 系统在没有启动 NFS 服务的情况下尝试挂载远程网络文件系统 `(NFS)` 卷。

当我们当前运行级别的所有系统服务都启动后，`init` 会启动图形化登录（因为我们处于运行级别 5）。图形化登录的定义出现在 `/etc/inittab` 的末尾，如下所示：

`# Run xdm in runlevel 5`

此示例显示了当 Fedora 启动到运行级别 5 时，`pre-fdm` 壳脚本会执行正确的 X11 显示管理器。

## 使用 GRUB 启动到非默认运行级别

在你选择了一个默认运行级别后，每次从关机状态重启系统时，都会选择该运行级别。可能会出现你不希望启动到运行级别的情况。你可能想要进入维护模式，或者在没有活动 X 服务器和图形化登录的情况下启动系统，以便修改或修复 X 服务器或桌面管理器。如果你使用 GRUB（Fedora 的默认引导加载程序），必须遵循几个步骤才能启动到非默认运行级别。

> 如果你启用了 GRUB 密码，必须先按 `p`，输入密码，然后按 `Enter` 才能使用此启动方法。

GRUB 引导加载程序在启动时向内核传递参数或命令。这些参数被用于告诉 GRUB 内核所在的位置，并向内核传递特定参数，例如可用内存量或是否应该配置特殊硬件。

要覆盖默认运行级别，你可以按照如下方式为 GRUB 添加额外的内核参数：

- 在图形界面上，按 `(e)` 进行编辑，向下滚动选择内核，再次按回。按下空格键，输入单数字或 `1`（Fedora 也允许 `S` 和 `s`），然后按 `Enter`。
- 最后，按 `b` 启动，你将启动到运行级别 `1`，而不是 `/etc/inittab` 中列出的默认运行级别。

Fedora 包含了几个命令行和图形系统管理工具，你可以使用它们在不同的运行级别下启动、停止、重启或恢复各种服务。这些命令（在本章中讨论）通过根据需要重命名、删除或创建从 `/etc/rc.d/init` 到 `/etc/rc.d/*` 的符号链接来工作。许多管理员使用这些命令来更改每个 `/etc/rc.d/re` 目录下脚本的符号链接，而不是手动操作。

符号链接的位置也可能让人困惑。Red Hat（现在是 Fedora）传统上将它们放在一起，而 Linux 标准基础 `(LSB)` 要求它们现在位于其他地方。由于其他脚本引用了这些文件，要更改它们非常困难，因此 Fedora 将符号链接放在 LSB 指定的地方。

正如你所推料的，符号链接是系统管理员工具箱中非常强大的工具。

## 理解 init 脚本和初始化的最后阶段

每个 `/etc/rc.d/init.d` 脚本（或 init 脚本）包含决定在接收到 `start` 或 `stop` 值时做什么的逻辑。这种逻辑可能是一个简单的执行 `switch` 语句，例如所示：

```bash
case "$1" in

start)

  start

  ;

stop)

  stop

  ;

restart)

  restart

  ;

reload)

  reload

  ;

status)

  rhstatus

  ;

condrestart)

  [ -f /var/lock/subsys/smb ] && restart;

  ;

*)

  echo "Usage: $0 {start|stop|restart|status|condrestart}"

  exit 1

esac
```

虽然可以使用这些脚本来自定义系统从关机到运行的方式，而不必替换内核，但这种方法也意味着系统不需要完全停止即可启动、停止、升级或安装新服务。

注意，并非所有脚本都使用这种方法，可能会向服务脚本传递其他消息，例如 `restart`、`reload` 或 `status`。此外，并不是所有脚本都响应同一组消息（`start` 和 `stop` 除外，根据惯它们必须接受这两个操作），因为每个服务可能需要特殊的命令。

## 第 15 章 自动化任务

你可以使用现有的脚本作为示例编写自己的 init 脚本。在 `/usr/share/doc/initscripts/sysvinitfiles` 中也可以找到示例脚本，以及 Red Hat 编写的一份简短教程以及对 init 脚本中可用选项的简要说明。

在所有脚本运行之后，你的系统已配置完毕，所有必要的系统服务都已启动。如果你使用的是 5 以外的运行级别，`init` 过程的最后一个动作是启动用户 `shell`——`bash`、`tesh`、`tsh` 或可用的许多命令 `shell` 中的任何。`shell` 启动后你会在屏幕上看到登录提示。

## 启动时控制服务

当我们当前运行级别的所有系统服务都启动后，`init` 会启动图形化登录（因为我们处于运行级别 5）。图形化登录的定义出现在 `/etc/inittab` 的末尾，如下所示：

`# Run xdm in runlevel 5`

此示例显示了当 Fedora 启动到运行级别 5 时，`pre-fdm` 壳脚本会执行正确的 X11 显示管理器。

## 使用文本命令

传统上，命令行工具 `chconfig` 被用于在每个运行级别显示、诊断或更改（如 `/etc/rc.d/init` 所示）。例如，要列出运行级别 5 中开启的服务，可以将 `chconfig` 的输出传递给 `grep`：

```bash
# chconfig --list | grep '5'

anron      0:off 1:off 2:on 3:on 4:on 5:off
```
