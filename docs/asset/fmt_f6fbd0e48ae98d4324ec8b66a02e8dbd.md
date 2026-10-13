
这些选项将在启动时运行。

我们的许多课程在全国各地的酒店中进行，这要求要求使用笔记本电脑。在 PCMCIA 支持的早期，只有大品牌设备能够稳定工作，但在过去的几年里，对其他卡的支持已经不断增长。这并不意味着没有问题，但现在比 2000 年以前的问题要少得多。

## 练习 5-4

### 卸载网络卡，然后安装 PCMCIA 卡

在本次练习中，你需要一台带有 PCMCIA 端口和至少一张功能良好的 PCMCIA 卡（例如网卡）的笔记本电脑。如果你能找到无法工作或运行不良好的旧卡，也可以尝试使用。

警告：大多数笔记本制造商并不推荐此操作，因此请`自担风险`。这很可能会损坏系统。我们已经在教室的几台笔记本电脑上尝试过，我们知道它们是可以行的。但你的电脑可能不行！如果你的笔记本说明书中没有允许，`不要尝试此实验！`这是对你的最后警告。

当你从某些笔记本电脑上拔出网卡时，系统会发出高频的哔声。如果你向正在运行 Linux 的笔记本电脑插入 PCMCIA 卡，它应该会响两次：第一次是 `cardmgr` 服务识别到添加（如果识别则发出高音调，未识别则发出低音调），如果成功，另一次是卡片配置正确（高音调）或配置失败（低音调）。`请自担风险尝试。`

## 认证目标 5.04

### 高级电源管理 (APM) BIOS

高级电源管理 (APM) BIOS 主要负责监控和控制系统电池。这是一项通常用于笔记本电脑的可选服务。如果你想实现较新 PC 上可用的 BIOS 待机和悬挂（Suspend）模式，也可以在工作站和服务器上使用它。

需要运行的守护进程是 `apmd`。在你的系统中，`proc` 目录下会创建一个电池信息的文件：

```bash
# cat /proc/apm
1.9 1.2 0x07 0x01 0xff 0x80 -1 - ?
```

如你所见，这种格式并不易读。要以更易读的格式打印这些信息，只需执行 `apm` 命令即可：

```bash
# apm
AC on-line, battery status high: 100% (2:31)
```

`apmd` 守护进程可以根据 BIOS 反馈的电池状态配置为记录各种不同的内容。你可以设置当电池电量低于某个百分比水平时，`apmd` 将错误消息记录到 `syslog`。当达到此警告级别时，你让它向所有登录用户发送系统级消息。所有电池信息的更改都会通过 `syslog` 记录。要设置 `apmd`，你需要编辑 `/etc/sysconfig/apmd` 文件。

```bash
# cat /etc/sysconfig/apmd
APMD_OPTIONS="-p 10 -w 5 -W"
```

在这个示例中，`apmd` 被指示在电池电量每减少 10% 时将更改记录到 `syslog` 文件中 (`-p 10`)。如果电量低于 5%，`apmd` 将向 `syslog` 发送警报 (`-w 5`)。此外，所有登录用户将收到系统即将没电的通知 (`-W`)。

`apm` 日志分为四个部分：

- 放电率（百分比/分钟）。如果正在充电，则为负值。
- 自上次充满电以来，或自上次登录以来，取决于电池是否已充满。
- 电池剩余时间估计值。
- 电池剩余寿命百分比。

当 BIOS 告诉 `apmd` 守护进程有一个挂悬挂或待机调用时，它会立即调用 `sync`（立即将所有缓存的文件系统信息写入磁盘）。然后它将睡眠二秒并告诉 BIOS 继续

## 练习 5-5

### 拔掉笔记本电脑电源；检查 apmd

在本次练习中，如果你有一台安装了 Linux 的笔记本电脑，可以在拔掉电源插之前运行 `apm` 命令。之后，检查系统如何管理这种转换。你可以随时使用 `apm` 查询电池状态。

警告：虽然某些笔记本电脑支持此操作，但请`自担风险`。

## 272 第 5 章：高级安装

```
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
# 在每个运行级别下运行的任务
ud:conice:/sbin/update
# 捕获 CTRL-ALT-DELETE
-t3 -r now
ca:ctrlaltdel:/sbin/shutdown -f +h "Power Failure, SystemShutting Down"
# 停电
pf:powerfail:/sbin/shutdown -c
# 电恢复
pr:1234:powerkill:/sbin/shutdown -c "Power Restored,Shutdown Cancelled"
# 在标准运行级别下运行 getty
1:235:respawn:/sbin/mingetty1
2:235:respawn:/sbin/mingetty2
3:235:respawn:/sbin/mingetty3
4:235:respawn:/sbin/mingetty4
5:235:respawn:/sbin/mingetty5
6:235:respawn:/sbin/mingetty6
# 运行 X11（或其他显示管理器）
xdm 是 Red Hat 6.0 中的一个独立服务
x5:respawn:/etc/X11/prefdm -nodaemon
```

这种语法是 SystemV 语法，看起来很难阅读。然而，一旦你熟悉了它，就可以一眼看出整个文件。以下是文件中每一行的详细说明。

id:5:initdefault 此命令在系统完成启动脚本运行后将默认运行级别设置为 5。运行级别 5 的意义将在后文中讨论。

```
si:sysinit:/etc/rc.d/rc.sysinit
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

第一行 (`si`) 是系统初始化文件。将在下一节中进行详细讨论。第 10–16 行也是每个运行级别下运行的初始化脚本。

## 理解 /etc/inittab 273

关于 RC 脚本的更多信息请参见第 5 章。注意，在每个 RC 脚本运行完成之前，`init` 不继续执行。

```
ud::once://sbin/update
```

此命令在我们每次更改运行级别时都会运行。注意，当你没有指定运行级别，它将在每个运行级别下运行。

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now
pf::powerfail:/sbin/shutdown -f -h2 "Power Failure, SystemShutting Down"
pr:12345:powerwait:/sbin/shutdown -c "Power Restored, Shutdown\nCancelled."
```

这些都是特殊操作。第一行 (`ca`) 将在三秒后关闭系统并重启。第二行 (`pf`) 将在收到 SIGPWR 信号（通常来自即将耗尽的 UPS）两分钟后停止系统。第三行 (`pr`) 表示，如果在两分钟内（上行）恢复恢复（来自 UPS 的信号），则取消关机。注意应该取消关机的运行级别列表。

```
1:2345:respawn:/sbin/mingget tty1
2:2345:respawn:/sbin/mingget tty2
3:2345:respawn:/sbin/mingget tty3
4:2345:respawn:/sbin/mingget tty4
5:2345:respawn:/sbin/mingget tty5
6:2345:respawn:/sbin/mingget tty6
```

这些行配置了六个虚拟控制。注意级别 1（单用户模式）没有加载任何虚拟控制：

```
x:5:respawn:/etc/X11/prefm -nodaemon
```
