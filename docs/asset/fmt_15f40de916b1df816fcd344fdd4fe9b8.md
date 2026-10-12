
### 用户与场景指令

```
USER normal_lights on front_porch; on back_porch

SCENE tv_on on tv_set; dim living-room 10

USER night_lights dim front_porch; dim back_porch $1
```

第一个 `SCENE` 被分配名为 `blinker`，对单元 `A1` 关两次。`normal_lights` `USER` 使用之前的别名（`front-porch` 和 `back_porch`）来开启。`tv_on` `SCENE` 开启电视并调暗所在房间的灯光。也可以为 `SCENE` 和 `USER` 指令添加参数。例如，当以后运行 `night_lights` `USER` 时，`$1` 参数将被命令行提供的第一个选项替换。

# 识别日志文件

Heyu 不使用日志文件（`LOG_DIR NONE`）。但是，你可以将 `NONE` 替换为目录的完整路径（例如 `/home/chris/.heyu/`）。可以使用该日志文件监控 Heyu 活动，例如 Heyu 脚本启动时的指示以及这些脚本的输出。以下行显示了修改后的 `LOG_DIR` 选项在 `/home/chris/.heyu/` 目录日志中的外观：

```
LOG_DIR /home/chris/.heyu/
```

如果你已经将 Heyu 配置为你的用户的根（在 `/etc/heyu/x10.conf` 中），你可以将日志文件放在标准的系统日志目录 `/var/log`。

![](img/1b8a24a162893627b8005ac678b79236_225_0.png)

# 添加 SCRIPT

`SCRIPT` 指令是你配合 Heyu 一起使用的最强大的指令。通过定义 `SCRIPT`，你可以告诉 Heyu 寻找某些事件的发生（例如开启 `B1` 的 X10 信号），并通过运行 Linux 中的任何命令来做出响应。以下是 `x10config` 文件中的一个示例：

```
ALIAS doorbell B1

SCRIPT doorbell on : play $HOME/sounds/barking_dog.wav
```

在之前的示例中，`doorbell` 被分配给代码/单元 `B1`。然后 `SCRIPT` 说，如果开启 `doorbell`，则运行文件 `$HOME/sounds/barking_dog.wav` 的命令。`SCRIPT` 指令和启动条件（`doorbell on`）后面跟着两个冒号。在两个冒号之后，你可以输入任何喜欢的命令。

# 使用计划文件 (x10.sched)

你可以从计算机将计划文件上传到 `CM11A` 设备，以便从该设备直接发送计划的 X10 信号。这使得即使计算机关闭，你的 X10 也能继续工作。根据以下条目，使用了 `$HOME/.heyu` 中的 `x10.sched` 文件：

```
SCHEDULE_FILE x10.sched

# SCHEDULE_FILE normal.sched

# SCHEDULE_FILE vacation.sched
```

# 202 第三部分 — 家庭项目

你可以看到额外的计划文件被注释掉了，这意味着如果你愿意，可以创建并使用额外的计划文件。Heyu 在 `/etc/heyu/` 目录下提供了一个示例计划文件（`x10_schedule.sample`），你可以根据喜好对其进行修改。（创建计划文件的详细步骤将在本章稍后的部分介绍。）

## 设置模式

当 `MODE` 设置为 `COMPATIBLE`（兼容模式）时，计划文件设置为从当年 1 月 1 日开始运行，并有效期为 366 天。因此，计划将持续到闰年的 12 月 31 日，或其它年份的 1 月 1 日。这是默认设置，如下所示：

```
MODE COMPATIBLE # COMPATIBLE HEYU
```

设置为 `HEYU` 时，`CM11A` 运行在活动时钟模式，导致计划从上传计划的日期开始。你可以使用 `PROGRAM_DAYS` 指令来设置配置文件的有效天数。（如果你正在运行 HEYU 模式，使用 Windows 上的 ActiveHome 软件可能会产生问题，如果 ActiveHome 允许重置 `CM11A` 时钟从 1 月 1 日开始。）

Heyu 模式的优势是计划文件可以在过期时随时重新加载，并适用于后续 366 天（或后文描述的更短时间），而 `COMPATIBLE` 模式如果要在日期之后保持准确，必须精确在 1 月 1 日重新加载计划。

如下行所示，如果你处于 HEYU 模式，`PROGRAM_DAYS` 设置为 366 天（默认值）。当上传的计划中包含日出-日落事件时，将此值设置为较短的天数可以提供更好的的准确性。

```
PROGRAM_DAYS 366 # [1 到 366 天数]
```

## 设置经纬度

Heyu 需要你所在位置的经纬度以便计算计划文件中引用的黎明和黄昏时间。在创建需要这些信息的计划文件之前，可以省略它们。这些指令的格式在德克萨斯州骡鞋（Muleshoe）的示例所示：

```
LATITUDE N34:14

LONGITUDE W102:44
```

在示例中，`(N/E/W)` 前缀位于以度、分表示的变量值之前。（你可以从 Astrodient 网站 `www.astro.com/atlas` 查询你的经纬度。）

你还可以在 `$HOME/.heyu/x10config` 文件中设置其他指令。要查看其他可用指令的描述，请参考该文件中的注释，或输入命令 `man x10config` 读取配置文件的帮助页以获取完整列表。

## 2：运行 Heyu 命令

`heyu` 命令是使用 Heyu 的主要工具。有 70 多个 `he` 命令，可以完成各种操作，从管理（如监控和重置房屋代码）到通过直接发送 X10 信号（开启、关闭、调暗等）更改 Heyu 引擎的状态：

# 第 7 章 — 使用 X10 自动化家庭灯光和设备 203

你可以像我描述 BottleRocket 那样使用 Heyu；只需向 shell 脚本添加大量 `heyu` 命令，或从 `cron` 任务中启动它们。然而，Heyu 版本 2 有一个功能，可以直接将计划文件上传到 `CM11A` 设备，这样即使电脑关闭，你的 X10 计划命令也可以继续运行。

以下章节描述了使用 `heyu` 命令管理你 X10 活动的一些方法。

## 发送 X10 信号

`heyu` 命令能够请求 `CM11A` 能发送到 X10 设备的任何 X10 命令。这些命令可以包含你设置的任何别名作用于相关的房屋代码，或直接使用房屋代码。以下是一些示例：

```
$ heyu on F5

$ heyu off F3

$ heyu lightson F

$ heyu lightsoff F

$ heyu allon F

$ heyu alloff F
```

上一组命令说明了开启和关闭 X10 设备的各种方式。第一条命令开启 `F5` 单元。第二个命令关闭 `F3` 单元。接下来的两个命令分别开启和关闭房屋代码 `F` 的所有模块。接下来的两个命令开启和关闭房屋代码 `F` 的所有单元（灯光和电器）。

使用 `heyu` 调暗和调亮有多种方法。以下是一些示例：

```
# heyu dim F5 7

# heyu dim F3 9

# heyu bright F 4
```

前面的代码中，第一个命令根据当前亮度将 `F5` 的灯调暗 `7`。下一条命令从全亮度将 `F3` 的灯调暗 `9`。下一条命令从其当前状态将 `F9` 的灯调亮 `4` 个等级。`CM11A` 在全调暗和全亮之间提供 `1–22` 级亮度。

你可以尝试几个用于 Heyu 的直接命令。要查看完整列表，请输入 `man heyu`。

> 由 Charles Sullivan 设计的 Heyu 的一个目标是，让每个 `CM11A` 原生命令都有一个对应的命令，可以放入上传的宏中。结果，Heyu 实现了一些没用的命令。无用命令的示例是 `brightb`（在第一次调亮到全亮后再次调亮）。

![](img/1b8a24a162893627b005ac678b9236_227.png)

## 管理 Heyu

通过 `heyu` 命令的管理选项，你可以更改或检查 X10 活动的当前状态。以下是你作为管理员输入的命令示例：

```
$ heyu reset

$ heyu setclock

$ heyu status F7

$ heyu info
```
