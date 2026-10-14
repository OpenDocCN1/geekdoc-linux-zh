
- 在 18:00–23:00 之间随机播放音乐和电视频道

- 给送奶工发短信取消送奶

- 向家人发送假期提醒电子邮件

> 注意 无论你的安保安排如何，公开宣布你正在度假都没有好处。尽管有关窃贼监视 Twitter 动态以选择入室行窃时机的报道大多是无稽之谈（判断是否有人在家有更简单的方法），但也没有必要掉以轻心。

## 设置 mashmode

设置 `mashmode` 非常简单，因为它们由两个包含脚本的目录组成，一个用于模式启动时，另一个用于被其他模式取代时。请注意，如果假日模式被“工作”或“在家工作”取代，这里没有任何区别。首先创建新配置文件：

```text
mashmode create holiday
```

这将创建前面提到的目录：

```text
./etc/mode/holiday/onenter
./etc/mode/holiday/onexit
```

每个目录都以完全相同的方式处理，因此无论你是进入还是离开该模式，都会扫描目录中的文件，然后：

- 如果存在 `x10` 计划文件，它会作为新计划上传到你的 x10 设备

- 如果存在名为 `process` 的脚本，它会运行该脚本，并执行其中包含的任意命令

- 如果存在 `xmit` 目录，它会向指定对象发送消息

第三种情况很有趣。文件名指示使用哪种通道来发送消息（电子邮件、短信等），而文件内容则指示发送给谁以及消息内容。

```bash
$ cat etc/mode/holiday/onenter/xmit/sms
#mm/sms
#!/bin/bash
date +"We're off on holiday, beginning on the %dth %B"
```

如你所见，第一行是注释，包含接收消息的逗号分隔的用户名。文件的其余部分是一个脚本，用于确定要发送的消息。

如需查看支持哪些通道，可以使用：

```text
msgconduit list
```

## 例程

例程是一系列定时事件，从特定时刻开始，与传统脚本并无不同。一个“唤醒”脚本的示例，它会在早上为你准备好淋浴，可能如下：

```text
MINBIN=/usr/local/minerva/bin
sleep 0
$MINBIN/alarm 1
sleep 300
$MINBIN/homedevice default on bedroom
sleep 600
$MINBIN/homedevice default on shower
sleep 60
$MINBIN/homedevice default on shower_speaker
sleep 10
$MINBIN/report say shower calendar
sleep 1200
$MINBIN/say shower Hurry up
$MINBIN/homedevice default on shower_speaker
$MINBIN/homedevice default on shower
$MINBIN/homedevice default on bedroom
```

这是由 cron 间接触发的，并带有多个内部定时，以应对从卧室到淋浴间的路程。与其编写直接的 crontab 行，例如：

```text
10 7 * * 1-5 /usr/local/minerva/bin/routine start 1
```

不如这样写：

```text
* * * * 1-7 /usr/local/minerva/bin/routine process
```

因为虽然它每分钟运行一次会带来更多处理开销，但它将控制权从 cron 中的（固定）脚本转移到 Minerva 配置目录中更具动态性的脚本。这使你可以在例程脚本中使用可变时间，因为 cron 不支持这些。例如，你可以根据实用脚本 `sunset` 的判定，在日落时自动开灯。

从结构上讲，描述例程过程的每个目录都包含四个文件：

```text
$ ls /usr/local/minerva/conf/routine/1
name normal days script
```

- `name` 是一行文本描述，人类可读，并显示在例程列表中

- `normal` 是该事件应被触发的正常时间，例如 7:00

- `days` 列出事件可以运行的日子，例如 sat,sun。因此，你需要创建两个不同的例程，分别处理周末和工作日的唤醒计划

- `script` 是在该时间运行的可执行文件

还有一个可选文件 `override`，如果存在，它会在第二天（且仅在第二天）使用其中包含的时间。第三天时间恢复到“正常”。这提供了一种简单的方式来实现“明天我得 6:00 起床，而不是 7:00，因为要开会”这样的概念，并消除了大量临时配置更改。

通过将脚本和时间与 cron 分离，你还可以：

- 以随机睡眠延迟开始，将事件延迟几分钟，让房屋感觉更人性化。

- 使用基于时间的处理器 `MTS`，查看你当前的位置，并禁用/启用各种事件。

- 检查天气，如果下雨并且它知道你会开车出行，则延迟闹钟，而不是叫醒你。

- 检查天气，如果下雪，它会提前叫醒你，因为它知道你需要更多时间来给车窗除霜。

- 检查火车时间，如果火车晚点，则延迟闹钟。或者如果火车取消，则自动给老板发电子邮件。

- 如果检测到你已经洗过澡，则阻止该事件（例如开始淋浴）发生。

这些用例可能涉及比正常时间更早或更晚启动某些事情。由于时间无法倒流，脚本应始终在事件最早适用时间触发，即最坏情况，并延迟事件直到最佳情况。这自然解决了“双重现实”问题：6 点的闹钟可能判定 7 点叫醒你可以接受……而 7 点的闹钟可能由于情况变化，决定应该依赖 6 点的事件来触发。

已知的规则例外（例如早间会议示例）仍然最好使用 `override` 文件来处理。

作为一个非常以开发者为中心的实现，这可以轻松地从 iOS 远程应用重新编程，或与日历关联。

最后，我展示一个来自我自己淋浴例程的真实示例！这个例程由我的“夜间”事件触发，并为我准备好淋浴。除了基本照明外，它还会向我读出第二天的日程安排。有趣的是，最后一点需要额外的逻辑，因为如果我在午夜后回家，那么“第二天”实际上就是同一天，我们需要相应调整流程：

```bash
# For early morning/late nights
if [ `date +%H` -le 4 ]; then
        REQUEST_DAY=today
        MESSAGE="Back late - I hope it was a good night. Let's talk about the morning"
else
        REQUEST_DAY=tomorrow
        MESSAGE="Let's talk about tomorrow"
fi

CONDUIT=vox
$MINBIN/report $CONDUIT shower echo $MESSAGE

# ... other messages here ...

$MINBIN/report $CONDUIT shower echo Let me look at the calendar
$MINBIN/report $CONDUIT shower calendar $REQUEST_DAY
$MINBIN/report $CONDUIT shower echo Checking house events
$MINBIN/report $CONDUIT shower latest $REQUEST_DAY
$MINBIN/report $CONDUIT shower weather $REQUEST_DAY
```

## Minty

`Minty` 有两个用途。首先，它是一个超时系统，设备自上次使用后三分钟内未被使用，将自动关闭。其次，它是一个引用计数工具，以确保第一个组件智能地运作。因此，如果两个人打开灯，它会在最后一个人关灯后三分钟关闭。这在自动化住宅中至关重要，因为可能一个人在现场打开它，另一个人远程打开它，计算机自动打开它……而这三方都会期望设备在他们与之交互期间保持开启。

为了实现这一点，每个设备都有一个 Minty 开启事件和一个相应的关闭事件，用两个脚本描述，例如：

```text
/usr/local/minerva/conf/minty/shower_speaker/on
/usr/local/minerva/conf/minty/shower_speaker/off
```

因此，当设备第一次需要开启时，会调用脚本 `minty start shower_speaker`，并记录时间。如果这是淋浴音箱第一次被打开，则运行上述脚本。如果不是，则其计数加一。一旦你使用完设备并将其关闭（使用意料之中的 `minty end shower_speaker` 命令），计数减一，如果计数达到零，三分钟超时开始。

因为开启脚本只在第一次调用时运行，所以你可以从许多不同位置触发同一事件。例如，淋浴音箱在以下情况下保持开启：

- 你在淋浴时播放音乐

- 正在听计算机语音朗读你的日历

- 淋浴灯亮着

这些事件触发器中的每一个都会对 `minty start shower_speaker` 进行相同的调用，因此只有当你停止在淋浴时听音乐、不再朗读日程并且关掉灯之后，它才会准备关闭。
