
# 204 第三部分 — 家庭项目

`heyu` 命令重置 `CM11A` 上的所有计数器并设置为配置文件中的默认房屋代码。`setclock` 选项将时间设置为你的电脑时间（使用本地时间），或 `HEYU` 中的偏移量。`status` 选项获取选取设备（例如 `F7`）的状态。`info` 选项显示 `CM11A` 内部寄存器维护的时间。

## 3：与 Heyu 状态引擎工作

`heyu` 命令可以启动 `heyu state engine`（守护进程），维护所有 `X10` 模块状态的记录（基于发送到每个模块的信号）。状态引擎的消息发送到该文件。

配合引擎，你可以打开 `heyu monitor` 来监控发送到 `CM11A` 设备的事件。如果你从命令行启动监控，可以从屏幕（标准输出）查看或将其重定向到文件。然而，如果识别到相同的输出将发送到你的日志文件。

要启动（或重启）`heyu` 状态引擎，输入：

```
$ heyu engine
```

要查看 `heyu` 引擎正在运行，输入：

```
$ ps aux | grep heyu

0 0 0.2 tty S+ 15:03:00 heyu_relay

0 0 0.2 tty S 15:32:00
```

你可以看到 `heyu_relay` 和 `engine` 正在后台运行。对于下一步，建议准备两个终端窗口。在第一个窗口输入以下命令监控 `X10` 活动：

```
$ heyu monitor
```

现在，在第二个终端（命令行）输入几个 `heyu` 命令来开启或关闭灯。例如：

```
$ heyu on A3
```

在运行 `heyu monitor` 的终端中，你应该看到发送到单元 `A3` 的命令。状态如下：

```
2005/01/01 07:52:39 send 3 : housecode A (tv_set)
2005/01/01 07:52:39 send On : housecode A
```

这说明了 `X10` 的基本组成：首先指定一个模块（或模块）；然后发送操作该房屋代码中所有模块的函数。在这个示例中，地址代码发送到了房屋代码 `A`，单元 `3 (A3)`。因为 `x10config` 文件中 `A3` 有别名（在这种情况下为 `tv_set`），你也可以看到它。（某些命令如 `alloff` 和 `lightson` 不需要你指定单个单元。）

![](img/1b8a24a162893627b005ac678b9236_228.png)

# 第 7 章 — 使用 X10 自动化家庭灯光和设备 205

`heyu` 标记指示了来自命令行的信号来源。`CM11A` 接口从交流电源接收到的信号在监控中通过标记识别。要监控你的 `X10` 活动，只需按 `Ctrl+C`。要关闭状态引擎，输入：

```
$ heyu stop
```

## 第四步：创建和上传计划文件

`Heyu` 计划文件提供了一种在文件中预设 `X10` 活动的方法，该文件可以上传到 `CM11A` 设备的 `EEPROM` 内存中。有了计划文件，你不需要一直开启电脑来继续你的 `X10` 活动。

你可以从复制 `Heyu` 软件包自带的计划文件（`x10.schedule.sample`）并对其编辑开始。例如：

```
$ cd $HOME/etc/heyu/x10.schedule.sample
# cp /etc/heyu/x10.schedule.sample x10.schedule
# vi x10.schedule
```

`Heyu` 文件中的语句有三种：宏（`macros`）、触发器（`triggers`）和定时器（`timers`）：

- `macro`（宏）：这些语句定义了通过电源线传输的 `X10` 序列。
- `trigger`（触发器）：这些语句指定了在电源线收到特定的 `X10` 开启或关闭信号时执行特定的宏。
- `timer`（定时器）：这些语句指定了要执行特定宏及其执行时间。

以下是这些语句的示例：

```
macro patio_on 0 on A1; dimb A3 6
macro 0_patio_off off 0 minutes; off A2; off A3
timer socalled 05/01-11/30 dusk:30 22:00 patio_on on patio_off
trig B1 on patio_on
trig B1 off patio_off
```
