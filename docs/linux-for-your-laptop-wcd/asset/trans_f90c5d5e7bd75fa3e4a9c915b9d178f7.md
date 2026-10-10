
## 显示和设置时间

从 Linux 中获取并显示日期和时间相对简单。一段简短的 C 程序可以快速检索并打印日期和时间。示例如下：

```c
#include <stdio.h>
#include <time.h>

int main()
{
	time_t now;

	time(&now);
	fputs(ctime(&now), stdout);
	return 0;
}
```

如果你将上述代码写入一个名为 `qd.c` 的文件中，就可以构建该程序，并将其命名为 `qd`：

```bash
# gcc -o qd qd.c
```

然后，你可以像这样运行 `qd`：

```bash
# ./qd
Wed Mar 22 10:18:16 2000
```

请注意，按下 Enter 键后，你将看到当前的日期和时间。然而，为了检查系统时间是否与时间匹配或相对于笔记本硬件时钟的时间是否正确偏移，请使用 `hwclock` 命令及其 `--show` 选项：

```bash
# /sbin/hwclock --show
Wed Mar 22 10:19:17 2000  -0.497501 seconds
```

在此示例中，Linux 系统时间被设置为与笔记本的硬件时钟相匹配。你可以使用 `hwclock` 命令，通过其 `--set` 和 `--date` 选项手动设置硬件时钟，如下所示：

```bash
# /sbin/hwclock --set --date "12/25/00 21:03:00"
```

按下 Enter 键后，硬件时钟将被设置为 2000 年 12 月 25 日下午 9:03。`hwclock` 命令可以使用 `--systohc` 或 `--hctosys` 选项将日期和时间值从 Linux 系统时间传输到笔记本的硬件时钟，或者反向传输。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_389_0.png)

图 16.1 *使用 Red Hat 的* `timetool` *命令设置你的 Linux 日期和时间*

Red Hat、Mandrake 和 Yellow Dog Linux 都包含 Red Hat 的 `timetool` 客户端。此命令要求你运行 X11。你可以通过 X11 终端窗口的命令行像这样启动它：

```bash
# timetool &
```

按下 Enter 键后，你会看到图 16.1 中所示的对话框。你可以使用它来设置日期和时间。

另一个你可以从控制台用来设置系统日期和时间的命令是 `date` 命令。在其最简单的形式中，使用 `date` 命令后跟月份、日期、小时和分钟，如下所示：

```bash
# date 03221200
```

Wed Mar 22 12:00:00 EST 2000

按下 Enter 键后，`date` 命令会显示你的新系统时间。

## 跟踪你所在时区

Red Hat 和 Yellow Dog Linux 使用符号链接 `/etc/localtime` 来指定你当前的时区。此链接指向 `/usr/share/zoneinfo` 目录下所需的时区数据库文件。在 Mandrake Linux 下，`/etc/localtime` 可能是实际时区数据库文件的副本。你可以使用 `ls` 命令像这样查看该文件是否为链接：

```bash
# ls -l /etc/localtime

lrwxrwxrwx 1 root root 32 Feb 17 1999 /etc/localtime -> ../usr/share/zoneinfo/US/Eastern
```

在此示例（来自 Red Hat 系统）中，时区被设置为 EST，即美国东部标准时间（Eastern Standard Time）。

当你启动 Linux 时，`/etc/rc.d/rc.sysinit` 系统初始化脚本使用 `hwclock` 命令来设置系统时间。`hwclock` 命令的选项保存在 `/etc/sysconfig/clock` 文件中，并使用如下设置：

```ini
ZONE="US/Eastern"
UTC=false
```

你可以手动修改此文件，创建自己的符号链接，或者使用 Red Hat 的 `timeconfig` 命令来设置时区。此命令可以作为 root 从控制台或 X11 终端窗口的命令行运行：

```bash
# timeconfig
```

按下 Enter 键后，你会看到图 16.2 中所示的对话框。

使用 Tab 键移动不同的按钮，使用上下光标键选择时区。使用空格键切换硬件时钟设置为 UTC。在完成选择后，导航到 OK 按钮并按下 Enter。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_390_0.png)

图 16.2 使用 Red Hat 的 `timeconfig` 命令设置你笔记本的当前时区。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_391_0.png)

**图 16.3** *使用 KDE 的 kmclock 客户端设置你笔记本的当前日期、时间和时区。*

如果你使用 KDE，请使用 `kmclock` 客户端设置不同的时间和时区。此客户端要求你运行 X11。点击面板上桌面的应用程序启动器按钮，然后选择“设置”、“日期和时间”。你也可以（作为 root）在 X11 终端窗口的命令行中输入 `kmclock` 并按 Enter 来启动客户端。你会看到图 16.3 中所示的对话框。

此客户端的优势在于能够在一个对话框中设置日期、时间和时区（尽管你必须点击“时区”选项卡来设置时区）。与 Red Hat 的 `timeconfig` 命令不同，`kmclock` 的时区不以位置名称列出，而仅以相对于 GMT（格林尼治标准时间）的偏移量或 0 表示。

## TZ 环境变量

Linux 还识别 `TZ` 环境变量，这是由你的 shell 保留在内存中的设置。你可以使用此变量告知从 shell 启动的其他应用程序当前使用什么时区。例如，你可以使用 `bash` shell 的 `export` 命令即时设置此变量：

```bash
# export TZ=EST+5
```

这将时区设置为 EST，且不包含夏令时。若要指定夏令时（DST），请使用 `TZ` 变量的额外字段，如下所示：

```bash
# export TZ=EST+5EDT,M4.1./M1.0.,5.0
```

## 获取精确时间

你可能根据其他时钟设置你的手表和钟表。如果你在家，快速查看一下你不同的时钟、手表、收音机、立体声或录像机，看看它们是否都显示相同的时间。很可能它们不一致！如果情况如此，你如何将精确的时间设置输入到你的笔记本硬件和 Linux 系统中？

如果你已连接到互联网，获取正确时间的一种方法是浏览许多发布当前时间（本地及其他时区）的网站之一，例如由美国商务部和美国国家标准与技术研究院赞助的 http://www.time.gov/。

然而，为 Linux 获取和设置时间的最佳方式是使用 `rdate` 命令（作为 root）。你需要有一个活动的互联网连接，使用 `rdate` 命令的 `-s`（设置）选项，并指定远程时间服务器的主机名。例如：

```bash
# rdate -s time.nist.gov
```

此命令通过从远程服务器检索时间信息来设置你的 Linux 系统时间。如果你只想显示时间，请像这样使用 `rdate` 命令：

```bash
# rdate time.nist.gov
[time.nist.gov] Wed Mar 22 13:56:23 2000
```

可以将 `rdate -s` 命令放入系统的 `/etc/crontab` 文件中，以便在笔记本连接到互联网时定期更新时间。一旦在本地服务器上维持了精确时间，就可以使用 `timed` 守护进程为网络的其余部分提供时间服务。`timed` 守护进程既可作为服务器也可作为客户端运行。如果你使用 `-x` 标志启动守护进程，它将成为主服务器，并向由 `-r` 选项指定的其他主机提供服务。例如，在服务器上，你可能会使用：

```bash
# timed -M -F stinky vaio green
```

然后，远程计算机（也许是一台或两台笔记本）stinky、vaio 和 green 应该不加选项地运行 `timed` 守护进程，如下所示：

```bash
# timed
```

此软件的一个有趣特性是，如果主时间服务器停止运行或无响应，其他主机将选举一个新的主服务器！

用于在网络上同步时间的另一个守护进程是 `xntpd` 守护进程，它通过网络时间协议（NTP）提供时间。但是，你需要有无线电、卫星接收器或调制解调器才能设置并提供服务。

要开始了解 NTP 和 xntpd，请查看 `/usr/doc/xntpd` 目录下的内容，并使用纯文本的 lynx 网页浏览器像这样操作：

```bash
$ lynx /usr/doc/xntpd*/index.html
```

没有网络访问权限？你可以通过电话收听最新时间，拨打美国海军天文台的 Master Clock Voice Announcer 电话：(202) 762-1401 或 (202) 762-1069。你还可以通过拨打 900-410-TIME 进行长途通话（这样就不必担心卫星延迟）；但是，首分钟收费 0.50 美元（美国），之后每分钟额外收费 0.45 美元（美国）。

## 有用的客户端

移动 Linux 用户对提供大量信息且体积小、节省屏幕空间并减少桌面杂乱的客户端情有独钟。KDE 用户知道，日期和时间默认显示在桌面面板的右下角。如果你看不到日期和时间，说明你的屏幕分辨率太小，你应该将面板重新配置为“tiny”设置（使用面板上的“配置”菜单项）。

Linux 还附带许多不同的时钟和日历客户端。你可以快速组合基于文本的 `cal` 命令的输出与 `xmessage` X11 客户端，制作自己的弹出式当月日历，如下所示：

```bash
$ cal | xmessage -geometry +1-0 -file - -title "Calendar"&
$ cal | xmessage -geometry +1+0 -file - -title "Calendar"&
$ cal | xmessage -geometry -1+0 -file - -title "Calendar"&
$ cal | xmessage -geometry -1-0 -file - -title "Calendar"&
```

无论屏幕分辨率如何，这些命令行都会在桌面的左下角、左上角、右上角或右下角生成一个小日历，如图 16.4 所示。

如果你正在旅行，并且需要确保不要吵醒地球另一端的人，请尝试 KDE 的 `kworldwatch` 客户端。此客户端可以从 KDE 的工具菜单或 X11 终端的命令行启动，如下所示：

```bash
$ kworldwatch &
```

按下 Enter 键后，你会看到图 16.5 中所示的窗口。它显示本地时间、UTC 时间、时区时间以及地球的墨卡托投影，显示日出和日落的分界线。

