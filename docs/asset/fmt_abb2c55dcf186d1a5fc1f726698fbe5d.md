
```bash
cat > /etc/sysconfig/console << "EOF"

# Begin /etc/sysconfig/console

UNICODE="1"

KEYMAP="de-latin1"

KEYMAP_CORRECTIONS="euro2"

LEGACY_CHARSET="iso-8859-15"

FONT="LatArCyrHeb-16 -m 8859-15"

# End /etc/sysconfig/console

EOF
```

某些键 `map` 具有死键（即本身不产生字符的键，但会在下一个键产生的字符上加上重音符号）或定义了组合规则（例如：默认键 `map` 中的“按下 Ctrl+. A 以获得 Æ”）。`Linux-4.9.9` 仅当组合的源字符不是多字节时才在内核中正确解释死键和组合规则。这种缺陷影响了欧洲语言的键 `map`，因为重音被添加到无重音的 ASCII 字符上，或者 ASCII 字符组合在一起。然而在 UTF-8 中这是一个问题，例如对于希腊语，需要在字母“alpha”上加上重音。解决方案是避免使用 UTF-8，或者安装在输入处理上没有此限制的 X 窗口系统。

- 对于中文、日语、韩语和其他语言，Linux 控制台无法配置为显示所需的字符。需要此类语言的用户应该安装 X Window 系统、涵盖必要字符范围的字体以及正确的输入法（例如 `SCIM`），它支持多种语言。

> 注意
> `/etc/sysconfig/console` 文件仅控制 Linux 控制台的本地化。通过设置正确的键盘布局来控制。

## 7.6.6 创建文件

`/etc/sysconfig/console` 文件仅控制 Linux 控制台的本地化。通过设置正确的键盘布局来控制。在启动时创建文件，这可以通过 `/sysconfig/console` 默认文件实现。

## 7.6.7 配置 syslogd 脚本

`syslogd` 脚本调用 System V 初始化。默认情况下，每隔 20 分钟写入时间戳。要关闭此时间戳，将 `SYSLOGD_PARMS` 设置为空值：

```bash
SYSLOGD_PARMS=
```

## 7.6.8 rc.site 文件

`/etc/sysconfig/console` 文件包含了在启动时自动设置的设置。它可以交替设置主机名、控制台文件。如果在独立文件中存在相关变量，`rc.site` 具有优先级。

```bash
# rc.site

#发行版信息

# 这些值在此指定将覆盖默认值

DISTRO="Linux From Scratch" # 发行版名称

DISTRO_CONTACT="lfs-dev@linux.org" # 报告地址

DISTRO_MINI="IFS" # 用于文件名的短名称
```

```bash
# 在不等待 udev 等 settle 的情况下加速启动
#OMIT_UDEV_SETTLE=y

# 在不等待 udev_retry 等待 settle 的情况下加速启动
#OMIT_UDEV_RETRY_SETTLE=yes

# 如果为 yes 则跳过清理 /tmp
#SKIPTMPCLEAN=no

# 用于 setclock
#UTC=1
#CLOCKPARAMS=

# 用于 consolelog（注意：默认值 7=debug，会有大量输出）
#LOGLEVEL=7

# 用于网络
#HOSTNAME=mylfs

# 关机时 TERM 和 KILL 信号之间的延迟
#KILLDEAY=3

# 可选的 syslogd 参数
#SYSLOGD_PARMS="-m 0"

# 控制台参数
#UNICODE=1
#KEYMAP="de-latin1"
#KEYMAP_CORRECTIONS="euro2"
#FONT=1at0-16 8859-15
#LEGACY_CHARSET=
```

## 7.6.8.1. 自定义启动和关机 Shell

LFS 的启动脚本和关机系统以相当高效的方式运行，但你可以在 `rc.site` 文件中进行两项调整，以进一步提高速度并根据你的喜好调整消息。要实现这一点，请调整 `/etc/sysconfig/rc.site` 文件中的设置。

- 在启动脚本 `udev` 期间，会调用 `udev` `settle`，这需要一些时间来完成。这个时间取决于或可能取决于系统中的设备。如果你只有分区和一个以太网卡，该过程可能不会进行等待。要跳过此过程，请设置变量 `OMIT_UDEV_SETTLE=y`。
- 启动脚本 `udev_retry` 默认也会运行 `udev` `settle`。只有当 `/var` 目录单独挂载时，才需要此命令。如果时钟是 `/var/lib/hwclock/adjtime` 文件。其他自定义可能也需要等待 `udev` 完成，但在许多安装中这是并不需要的。通过设置变量 `OMIT_UDEV_RETRY_SETTLE=y` 可以跳过该命令。
- 默认情况下，文件系统检查是静默的。这在启动过程中可能表现为延迟。要开启 `fsck` 输出，请设置变量 `VERBOSE_FSCK=y`。
- 重启时，你可能想完全跳过文件系统检查 `fsck`。要这样做，要么创建 `/fastboot` 文件，要么现在使用命令 `/sbin/shutdown -f` 重启系统。相反，你可以通过 `/forcefsck` 或运行 `shutdown` 时使用 `-F` 代替 `-f` 来强制所有文件系统进行检查。

设置 `FASTBOOT=y` 将在启动过程中禁用 `fsck`，直到其移除。不建议长期这样做。

- 通常，`/tmp` 目录下的所有文件在启动时会被删除。取决于文件或目录的数量，这可能会导致启动过程出现明显的延迟。要移除这些文件，设置变量 `SKIPTMPCLEAN=y`。
- 在启动期间，`init` 程序会向它启动的每个进程（例如 `agetty`）发送 `TERM` 信号，等待设定的时间（3 秒），然后向每个进程发送 `KILL` 信号并再次等待。此过程对于所有未由其自己的脚本关闭的进程都会重复执行。`init` 中的延迟可以通过传递参数来设置。例如，在关机或重启时设置 `-0` 参数以移除 `init` 中的延迟（例如 `/sbin/shutdown -o -r now`）。通过设置参数 `KLLDELAY=0` 可以缩短 `sendsignal` 脚本的延迟。

## 7.7 Bash 启动文件

程序 `/bin/bash`（以下称为“shell”）使用一组文件来帮助创建运行所需的环境。每个文件都有特定的用途，并可能以不同的方式影响登录和交互式环境。`/etc` 目录下的文件提供全局设置。如果你的家目录中存在等效文件，它可能会覆盖全局设置。

交互式登录 `shell` 在成功登录后，使用 `/bin/login` 通过读取 `/etc/passwd` 文件启动。交互式非登录 `shell` 在命令行处启动（例如 `[prompt]$bin/bash`）。当 `shell` 运行时，通常会存在一个非交互式 `shell`。它是非交互的，因为它正在处理脚本，而不是在等待用户输入命令。

欲需更多信息，请参阅“Bash Startup Files and Interactive Shells”章节中的 `info bash`。

当 `shell` 被作为交互式登录 `shell` 调用时，会读取 `/etc/profile` 和 `~/.bash_profile`。设置这些文件并正确设置某些环境变量会导致：

- 程序的输出翻译为本地语言
- 字符正确分类为字母、数字和其他类别。这对于 `bash` 在非英语区域设置的命令行中正确接受非 ASCII 字符是必要的
- 该国家正确的字母排序顺序
- 适当的默认纸张大小
- 金钱、时间和日期值的正确格式

将 `<ll>` 替换为所需语言的两个字母代码（例如 "en"），将 `<CC>` 替换为相应国家的两个字母代码（例如 "GB"）。`<charmap>` 应被替换为所选区域的标准字符集。可能还存在可选的修符（如 "@euro"）。

通过运行 `locale -a` 可以获取 Glibc 支持的所有区域列表。（此处省略了原文中大量重复的 OCR 识别错误文本）。

以下是一个通用的 `inputrc` 文件，并附有解释各种选项作用的注释。注意，注释不能与命令在同一行。使用以下命令创建该文件：

```bash
cat > /etc/inputrc << "EOF"

# Begin /etc/inputrc

# Modified by Chris Lynn <rory@rory.dynup.net>
```

```bash
# 允许命令提示符换行到下一
set horizontal-scroll-mode Off
```

```bash
# 启用 8 位输入
set meta-flag On
set input-meta On
```

```bash
# 关闭第 8 位剥离
set convert-meta Off
```

```bash
# 保留第 8 位用于显示
set output-meta On
```

```bash
# 无、可见或听觉提示
set bell-style none
```

```bash
# 以下所有内容都将 lst 参数中值的转义序列
# 映射到 readline 特定函数
```
