
## 协调世界时 (UTC)
UTC 是世界协调时间的标准。UTC 是英国伦敦格林尼治皇家天文台的当前平太阳时。因此，UTC 也被称为`格林尼治标准时间`（GMT）。你的本地时间是通过从 UTC 加上或减去每个时区差一小时或零来确定的。例如，我居住的地方距离格林尼治七个时区，所以我的时间是 UTC –7。因此，当我本地时间是上午 10:58 时，UTC 时间是下午 5:58。如果你的硬件时钟设置为 UTC 而非本地时间，你需要将`/etc/sysconfig/clock`文件中的`HWCLOCK`指令设置为`–u`。你的 Linux 系统将根据你的本地时区自动计算夏令时偏移量。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_210_1.png)

**注意** 对于 Linux 系统，实际上建议你将硬件时钟设置为 UTC 而非本地时间。

## 本地时间
在大多数你会遇到的系统中，硬件时钟默认设置为本地时间。如果情况如此，`/etc/sysconfig/clock`文件中的`HWCLOCK`指令将被设置为`–localtime`。

在处理 Linux 系统时，将硬件时钟设置为 UTC 是首选选项。使用 UTC 使计算时区差异变得更加容易。事实上，如果你在 Linux 系统上安装某些群件应用程序，可能会要求你将硬件时钟设置为 UTC，因为这便于在位于不同时区的众多计算机之间协调时间戳。

### 配置时区
在初始安装 Linux 系统时，系统会提示你指定系统所在的时区。在某些发行版（如 Ubuntu）中，你指定的时区保存在`/etc/timezone`文件中。你可以在 Shell 提示符下使用`cat`命令显示该文件的内容，以查看系统的当前时区。例如：

```bash
tracy@ws1:~$ cat /etc/timezone
America/Denver
```

其他发行版（如 openSUSE）则将此信息保存在`/etc/sysconfig/clock`文件中。该文件中的`TIMEZONE=`指令用于配置要使用的区域文件，如下所示：

```bash
TIMEZONE="America/Boise"
```

你也可以通过在 Shell 提示符下输入`date`来查看当前时区，如下所示：

```bash
ws1:~ # date
Wed Feb  9 11:40:05 MST 2011
ws1:~ #
```

如果需要在安装后更改时区，你可以在 Shell 提示符下使用`tzselect`或`tzconfig`命令。基于 Debian 的发行版使用`tzconfig`命令，而其他发行版（如 openSUSE 和 Fedora）使用`tzselect`命令。此命令必须以 root 用户身份运行。示例如下：

```bash
ws1:~ # tzselect
Please identify a location so that time zone rules can be set correctly.
Please select a continent or ocean.
1) Africa
2) Americas
3) Antarctica
4) Arctic Ocean
5) Asia
6) Atlantic Ocean
7) Australia
8) Europe
9) Indian Ocean
10) Pacific Ocean
11) none - I want to specify the time zone using the Posix TZ format.
```

`tzselect`命令首先显示大陆和海洋列表。请输入你想要切换到的时区所在地区的相应数字。输入后，将显示该地区国家的列表。请输入系统所在国家的数字；然后输入相应时区的数字。系统会提示你确认时区更改，如以下示例所示：

```bash
The following information has been given:
    United States
    Mountain Time

Therefore TZ='America/Denver' will be used.
Local time is now:  Wed Feb  9 11:50:10 MST 2011.
```

Universal Time is now: Wed Feb 9 18:50:10 UTC 2011.

- 1) Yes
- 2) No
- #?

如果更改正确，请输入 1 进行确认。注意，在上述示例中，`tzselect`通过设置`TZ`环境变量的值来切换时区。实际上，你可以在不使用`tzselect`的情况下，通过设置`TZ`环境变量的值并将其导出，从 Shell 提示符下更改时区。这在以下情况下非常有用：你没有系统的 root 密码，或者你想为你的账户使用不同的时区，而不改变其他用户使用的时区。语法为`export TZ=time_zone`。可用时区的列表可以在`/usr/share/zoneinfo/`目录中找到，如下所示：

```bash
ws1:~ # ls /usr/share/zoneinfo/
Africa        Canada        Factory       Iceland     MST7MDT     Portugal    Zulu
America       Chile         GB            Indian      Mexico      ROK         iso3166.tab
Antarctica    Cuba          GB-Eire       Iran        Mideast     Singapore   posix
Arctic        EET           GMT           Israel      NZ          Turkey      posixrules
Asia          EST           GMT+0         Jamaica     NZ-CHAT     UCT         right
Atlantic      EST5EDT       GMT-0         Japan       Navajo      US          zone.tab
Australia     Egypt         GMT0          Kwajalein   PRC         UTC
Brazil        Eire          Greenwich     Libya       PST8PDT     Universal
CET           Etc           HST           MET         Pacific     W-SU
CST6CDT       Europe        Hongkong      MST         Poland      WET
ws1:~ #
```

请注意，此更改不是持久的。如果你重启系统，时区更改将会丢失。你可以将以下行添加到用户主目录中的`.profile`文件，使时区更改对你的用户账户保持持久化：

```bash
export TZ='America/Denver'
```

你还可以使用`/etc/localtime`文件以及我们在前面看过的`/usr/share/zoneinfo`中的各种区域文件来更改时区。为此，请从`/etc/localtime`创建一个指向`/usr/share/zoneinfo`中相应时区文件的符号链接。例如，如果你想切换到美国的山区标准时间（MST）时区，你将在 Shell 提示符下输入`ln -sf /usr/share/zoneinfo/MST /etc/localtime`。

> **注意** 常用的文本编码包括`iso8859`（也称为 Latin-9 编码），它专为西欧语言设计；`ASCII`，使用基于英语的字符编码方案；以及`Unicode`，它旨在处理来自世界各地语言的字符集。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_212_0.png)

### 章节复习
在本章中，我强调了在实施新的 Linux 系统时创建部署计划的重要性。该计划中的第一个组件是进行需求评估。在进行需求评估时，你应首先确定项目目标并识别利益相关者。在实际启动项目之前，你应获得所有相关方的批准。你应该利用需求评估中收集的信息来制定项目范围，确切地说明

项目范围包括项目时间表、分配给项目的资源以及需要完成的任务范围。我指出，任何项目都涉及在进度、资源和规模三者之间进行三向平衡。这些因素中任何一项的变化都会导致另外两项的变化。
