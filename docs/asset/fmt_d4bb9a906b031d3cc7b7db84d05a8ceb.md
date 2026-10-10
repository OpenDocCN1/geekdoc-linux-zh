
## 欢迎进入紧急模式

登录后，输入 `journalctl -xb` 查看系统日志，输入 `systemctl reboot` 重启，输入 `systemctl default` 或 `^D` 尝试重新进入默认模式。

输入维护所需的 `root` 密码（或输入 `Control-D` 继续）：

```
# systemctl is-system-running

maintenance

# systemctl list-units --type=target
```

| UNIT | LOAD | ACTIVE | SUB | DESCRIPTION |
| :--- | :--- | :--- | :--- | :--- |
| `emergency.target` | loaded | active | active | Emergency Mode |
| [...] | | | | |

```
# systemctl default
```

在列表 6.16 中，注意你不需要为紧急目标单元文件名添加 `.target` 扩展。所有 `systemd` 目标都是如此。一旦进入紧急模式，你必须在提示符处输入 `root` 密码。一旦在命令行，你可以输入欢迎显示中列出的命令，或尝试一些额外的 `systemctl` 命令。

你可以切换的其他目标还包括 `reboot`、`poweroff` 和 `halt`。例如，只需输入 `systemctl isolate reboot` 即可重启系统。

注意列表 6.16 中，当执行 `systemctl is-system-running` 命令时，响应是 `maintenance` 而不是 `running`。此外，当使用 `list-units` 命令时，它显示 `emergency.target` 处于活动状态。`systemctl default` 命令将导致系统尝试进入默认目标。

如果你使用 `GRUB2` 作为引导加载程序，可以通过通常启动系统的菜单选项进入不同的目标，并按 `E` 键进行编辑。向下滚动找到以 `linux1` 命令开头的行。按 `End` 键到达行尾。按下空格键并输入 `systemd.unit=target-name target`，其中 `target-name` 是你想要激活的目标名称。这在紧急情况下非常有用。

一个实用的 `systemd` 组件是 `systemd-analyze` 工具。通过该工具，你可以调查系统的启动性能并检查潜在的系统初始化问题。表 6.8 包含了你使用 `systemd-analyze` 工具时更常用的命令。

# 第 6 章 维护系统启动与服务

## 表 6.8 常用 systemd-analyze 命令

| Command | Description |
| :--- | :--- |
| `blame` | 显示每个运行单元初始化所需的时间。单元及其时间按从慢到快的顺序列出。 |
| `time` | 显示系统初始化在内核和初始 RAM 文件系统上花费的时间，以及普通用户空间初始化所需的时间。（默认） |
| `critical-chain` | 以树状格式显示对时间敏感的单元。可以传递一个单元文件作为参数，将信息集中在该特定单元上。 |
| `dump` | 显示有关所有单元的信息。显示格式可能会在不通知的情况下更改，因此应仅供人类查看。 |
| `verify` | 扫描单元文件并在发现任何错误时显示警告信息。接受一个单元文件名作为参数。 |

下一节将为你提供足够的对 `SysV init` 的理解，以帮助 `Linux` 服务器迁移到 `systemd` 的过程。

## 理解运行级别 (Runlevels)

在系统启动时，`SysV` 并不使用目标（targets）来确定启动哪些组的服务，而是使用运行级别（runlevels）。这些运行级别定义在表 6.9 和表 6.10 中。注意不同的发行版使用的运行级别定义不同。

### 表 6.9 基于 Red Hat 的发行版 SysV init 运行级别

| 运行级别 | 描述 |
|---|---|
| `0` | 关闭系统。 |
| `1`, `s` 或 `S` | 用于系统维护的单用户模式。 |
| `2` | 未启用网络服务的多用户模式。 |
| `3` | 已启用网络服务的多用户模式。 |
| `4` | 自定义 |
| `5` | 带有 GUI 的多用户模式。 |
| `6` | 重启系统。 |

注意，从定义上来说，运行级别 `0` 和 `6` 并不是运行级别。它们表示从当前系统状态到目标状态的转换。例如，一个当前运行在运行级别 `5` 的系统通过运行级别 `0` 转换到关机状态。

### 表 6.10 基于 Debian 的发行版 SysV init 运行级别

| 运行级别 | 描述 |
|---|---|
| `0` | 关闭系统。 |
| `1` | 用于系统维护的单用户模式。 |
| `2` | 带有 GUI 的多用户模式。 |
| `6` | 重启系统。 |

要确定系统当前和之前的运行级别，你需使用 `runlevel` 命令。显示的第一个数字或字母表示上一个运行级别（`N` 表示系统新启动），第二个数字表示当前运行级别。列表 6.18 显示了一个新启动的基于 `Red Hat` 的 `SysV init` 系统的示例，该系统正运行在运行级别 `5`。

## 管理 SysV init 系统

### 列表 6.18：使用 runlevel 命令

```
# runlevel

N 5

#
```

`SysV init` 系统不是使用像 `systemd` 那样的默认目标，而是使用一个配置文件 `/etc/inittab`。该文件曾用于启动许多不同的服务，但在多年后的版本中，它只启动终端服务并定义系统的默认运行级别。

定义默认运行级别的文件行如列表 6.19 所示。

### 列表 6.19：设置默认运行级别的 /etc/inittab 行

```
# grep :initdefault: /etc/inittab

id:5:initdefault:
```

在列表 6.19 中，请注意 `/etc/inittab` 文件记录中 `id:` 和 `:initdefault:` 之间的数字 `5`。这表示系统的默认运行级别是 `5`。`initdefault` 指定了系统启动后要进入的运行级别。

> 回顾本章的表 6.1。你会发现 `systemd` 通过运行级别目标提供了对 `SysV init` 的向后兼容性，这些目标可以作为默认目标，并/或通过 `systemctl isolate` 命令在切换目标时使用。

设置默认运行级别配置某些服务在系统初始化时启动的第一步。接下来，每个服务都必须有一个初始化脚本，通常位于 `/etc/init.d/` 目录。列表 6.20 显示了该目录下各种脚本的片段。注意 `ls` 命令使用了 `-F` 选项以单列形式显示脚本并加上文件指示代码。`*` 文件指示代码表示这些是可执行程序（在此情况下为 `Bash` shell 脚本）。

### 列表 6.20：列出 /etc/init.d/ 目录下的脚本文件

```
# ls -F /etc/init.d/

anacron*

atd*

[...]

cronond*

cups*
```

### 列表 6.20：列出 /etc/init.d/ 目录下的脚本文件（继续）

```
[...]

tpd*

[...]\ypbind*

yum-updatesd*
```

这些初始化脚本负责启动、停止、重启、重新加载和显示各种系统服务的状态。调用这些初始化脚本的程序是 `rc` 脚本，它可以位于 `/etc/init.d/` 或 `/etc/rc.d/` 目录。`rc` 脚本运行特定目录下的脚本。该目录取决于所需的运行级别。每个运行级别在 `/etc/rc.d/` 目录中都有自己的子目录，如列表 6.21 所示。

### 列表 6.21：/etc/rc.d/ 目录中的运行级别子目录

```
# ls /etc/rc.d/

init.d rc0.d rc2.d rc4.d rc6.d rc.sysinit

rc rc1.d rc3.d rc5.d local*
```

注意列表 6.21 中，有七个名为 `rcn.d` 的子目录，其中 `n` 是 `0` 到 `6` 的数字。`rc` 脚本运行目标运行级别的 `rcn.d` 子目录下的脚本。例如，如果所需的运行级别是 `3`，则 `/etc/rc.d/rc3.d/` 目录下的所有脚本都会运行。列表 6.22 显示了该目录下脚本的片段。

### 列表 6.22：/etc/rc.d/rc3.d 目录下的文件

```
# ls -LF /etc/rc.d/rc3.d/

K0*

K1*

K2*

K3*

K4*

K5*

K6*

S0*

S1*

S2*

S3*

S4*

S5*

S6*
```

查看服务工具的运行示例会有帮助。列表 6.25 提供了几个供你参考。

### 列表 6.25：使用服务工具

```
# service httpd status

httpd is stopped

#

# service httpd start

Starting httpd: [ OK ]

#

# service httpd status
```
