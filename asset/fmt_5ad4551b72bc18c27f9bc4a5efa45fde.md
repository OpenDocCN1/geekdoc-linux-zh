
可选的 `/etc/sysconfig/rc.site` 文件包含每个 SystemV 启动时自动设置的配置。它也可以设置 `/etc/sysconfig/` 目录下 `hostname`、`console` 和 `clock` 文件中所指定的值。如果这些独立的文件和 `rc.site` 中存在关联变量，则特定文件中的值生效。

`rc.site` 还包含可以自定义启动过程其他方面的参数。设置 `IPROMPT` 变量将启用选择性启动。其他选项在文件注释中描述。该文件的默认版本为：

```
# rc.site
# 启动脚本的可选参数。

# 发行版信息
# 如果在此处指定了值，将覆盖默认值
#DISTRO="Linux From Scratch" # 发行版名称
#DISTRO_CONTACT=ifs-dev@lists.linuxfromscratch.org # 错误报告地址
#DISTRO_MINAME=LIFE # 发行版配置文件名使用的短名称

# 定义打印到屏幕上的消息使用的自定义颜色
# 更多信息请参阅 "man console_codes"
# 位于 "ECMA-48 Set Graphics Rendition" 章节
# 警告：当从 8 位字体切换到 9 位字体时，
# linux 将重新解释加粗 (i)；
# 9 位字体的前 26 个字形。这不会影响控制台

# 如果在此处指定了这些值，将覆盖默认值
#BRACKET=\u033[1;34m" # 蓝色
#FAILURE=\u033[1;31m" # 红色
#INFO=\u033[1;36m" # 青色
#NORMAL=\u033[0;39m" # 灰色
#SUCCESS=\u033[1;32m" # 绿色
#WARNING=\u033[1;33m" # 黄色

# 使用颜色前缀
# 如果在此处指定了这些值，将覆盖默认值
#BEMPTY_PREFIX=""
#SUCCESS_PREFIX="$(SUCCESS) * $(NORMAL)"
#FAILURE_PREFIX="$(FAILURE)***$(NORMAL)"
#WARNING_PREFIX="$(WARNING) *** $(NORMAL)"
```

```
# 手动设置消息输出的右边缘（字符）
# 有助于在启动期间重置控制台字体以覆盖
```

# 自动检测检测

#COLUMNS=120

# 交互式启动

#IPROMPT="yes" # 是否显示交互式启动提示

#timeout="3" # 显示提示符的时间（秒）

# 发行版窗口的总长度，不包含转义代码

#len=$(echo "Welcome to $DISTRO" | wc -c)

#welcome_message="Welcome to $(DISTRO)"

# 交互式字符串的总长度，不包含转义代码

#len=$(echo "Press 'I' to enter interactive startup" | wc -c)

#i_message="Press '$(FAILURE)\' to enter interactive startup"

# 设置脚本在重启时检查文件系统

#FASTBOOT=yes

# 跳过从控制台读取

#HEADLESS=yes

# 如果为是，则输出 fact 进度

#VERBOSE_FSCK=no

# 在不等待 udev settle 的情况下加速启动

#OMIT_UDEV_SETTLE=yes

# 在不等待 udev settle 的情况下加速启动

#OMIT_UDEV_SETTLE=yes

# 如果为是，则跳过清理 /tmp

#SKIMPCLEAN=no

# 用于 setclock

#UTC=1

#CLOCKPARAMS=

# 用于 ringconsole（注意默认值 7=debug，会有噪音）

#LOGCONLEVEL=7

# 用于网络

#HOSTNAME=myylfs

# 关机时 TERM 和 KILL 信号之间的延迟

#KILLEDELAY=3

# 可选的 syslogd 参数

#SYSLOG_PARMS="-m 0"

# 控制台参数

#UNICODE=1

#KEYMAP="de-latin1"

#KEYMAP_CORRECTIONS="euro2"

#FONT="lat0-16 -8859-15"

#LEGACY_CHARSET=
```

### 9.6.8.1. 自定义启动和关机脚本

LFS 启动脚本以相当的方式关闭系统，但你可以在 `rc.site` 文件中进行一些调整以进一步提高速度，并根据你的喜好调整消息。要为此，请调整上述 `/etc/sysconfig/rc.site` 文件中的设置。

在启动脚本 `udev` 中，对 `udev settle` 的调用需要一些时间。这取决于系统中的设备，可能不需要。如果你只有简单的分区和单个网卡，启动过程可能不会等待此命令。要跳过它，请设置变量 `OMIT_UDEV_SETTLE=.`。

启动脚本 `udev_retry` 默认也会运行 `udev settle`。只有当系统中的设备需要时才需要此命令。这取决于系统中的设备，可能不需要。如果你只有简单的分区和单个网卡，启动过程可能不会等待此命令。要跳过它，请设置变量 `OMIT_UDEV_SETTLE=.`。

（注：原文中 `udev_retry` 段落存在大量重复，已清理冗余重复，以在保持逻辑流畅的同时保留所需的内核内容。）

`"C"`（默认）和 `"en_US.utf8"`（美国英语用户的推荐设置）是区域设置（locales）。`"C"` 使用 US-ASCII 7 位字符集，并将高位设置为“开启”的字节视为无效字符。这就是为什么例如，`ls` 命令在在该区域设置下会将它们显示为问号。此外，从 Mutt 或 Pine 尝试发送带有此类字符的邮件将导致发送不符合 RFC 标准的邮件（Outlook 中的字符集显示为“unknown 8-bit”）。因此，只有在你确定永远不需要 8 位字符时，才能使用 `"C"` 区域设置。

许多知名程序并不支持基于 UTF-8 的区域设置。目前正努力记录并尽可能可能地修复这些问题。请参阅 https://www.linuxfromscratch.org/blfvs/view/11.3/introduction/locale-issues.html。

## 9.8. 创建 `/etc/inputrc` 文件

`inputrc` 文件是 `readline` 库的配置文件，该库在用户从终端输入行时提供编辑功能。它通过将键盘输入转换为特定操作来工作。`readline` 被 `bash` 以及其他 shell 以及许多其他应用程序使用。

大多数人不需要用户特定的功能，因此下面的命令创建了一个所有登录用户都使用的全局 `/etc/inputrc`。如果你以后决定按用户为单位覆盖默认设置，你可以在用户的家目录下创建一个带有修改后映射的 `.inputrc` 文件。

有关如何编辑 `inputrc` 文件的更多信息，请参阅 `info bash` 下的 `Readline It` 部分。`info readline` 也是一个很好的信息来源。

下面是一个通用的全局 `inputrc`，并附有解释各种选项作用的注释。注意，注释不能与命令共行。使用以下命令创建该文件：

```
cat > /etc/inputrc << "EOF"

# Begin /etc

# Modified by Chris Lynn koryo@koryo.dynup.net

# 允许命令提示符换换行

set horizontal-scroll-mode Off

# 启用 8 位输入

set meta-flag On

set input-meta On

# 关闭第 8 位剥离

set convert-meta Off

# 为显示时保留第 8 位

set output-meta On

# 无、可见或听见

set bell-style none

# 以下所有内容都将 lst 参数中包含的值的

# 转义序列映射到 readline 特定命令

"\Eo": backward-word

"\Eo": forward-word

# 用于 linux 控制台

"\E[1": beginning-of-line

"\E[4": end-of-line

"\E[5": beginning-of-history

"\E[6": end-of-history

"\E[3": delete-char

"\E[2~": quoted-insert

# 用于 xterm

"\eOH": beginning-of-line

"\eOF": end-of-line

# 用于 Konsole

"\E[H": beginning-of-line

"\E[F": end-of-line

# End /etc/inputrc

EOF
```
