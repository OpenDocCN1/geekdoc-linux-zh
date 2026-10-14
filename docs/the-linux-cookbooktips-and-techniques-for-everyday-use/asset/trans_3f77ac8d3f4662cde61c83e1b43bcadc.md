

Party at Jack's
Fri Lunch with Kim and Jo, 12:30
Mon Book manuscript due

据报道，`calendar` 工具首次出现在 AT&T UNIX 的第 7 版中，并在早期为 BSD 系列的 Unix 重写。虽然 BSD 衍生版本作为 `bsdmntutils` 软件包的一部分可用于 Debian，但该工具尚未成为所有 Linux 发行版的标准。

以下是编写日历文件的配方，包括在自己的日历文件中包含其他日历文件，以及自动提醒交付的方法。

> 注意：Emacs 也有此工具的等效功能，它称之为“日记”。有关此功能的更多信息，请参阅 Info 文件 `emacs-e20.info`，节点 `Diary`。

- 28.4.1 创建预约文件
- 创建输入日历文件。
- 28.4.2 在提醒中包含假日
- 在你的日历中包含其他日历。
- 28.4.3 自动预约交付
- 自动化你的预约交付。

## 28.4.1 创建预约文件

要开始使用 `calendar`，你需要创建一个“日历文件”来输入你的预约。它只是一个纯文本文件，可以命名为 `calendar` 或 `.calendar`；后者使其成为“隐藏”文件，如“列出隐藏文件”中所述。

将每个预约或日历条目单独写在一行；文件中的空行将被忽略。日历条目的格式如下：

```
[date] [tab or spaces] [text of reminder itself]
```

几乎所有常见的日期样式都被识别。例如，以下都是七月四日的有效日期：

```
7/4
July 4
4 July
Jul. 4
Jul 4
```

条目也不限于某一天；你也可以为一周中的某一天或某个月设置条目--- `Mon` 或 `Monday` 表示每周的每个星期一；`Jun` 或 `June` 表示每个六月的第一天。你可以使用星号作为通配符：`*/13` 会提醒你在每个月的十三号。当一行中省略日期时，则假定为前一个预约的日期。

例如，假设你在主目录中有名为 `calendar` 的文件，其内容如下：

```
6/16    Finish draft of book
        Party at Jack's
6/20    Gallery reading
Fri     Lunch with Kim and Jo, 12:30
Mon     Book manuscript due
```

如果当前日期是 6 月 16 日，星期五，并且你在主目录中运行 `calendar`，你将得到与上一节“管理预约”中的示例相同的输出。

> *注意：* 在上面的示例中，聚会的条目没有日期——它使用了前一个条目的日期，`6/16`。

## 28.4.2 在提醒中包含假日

`calendar` 软件包附带了许多种假日和其他场合的预制日历文件，你可以在自己的日历文件中引用它们，以将它们的条目包含在自己的提醒中。

预制文件存储在 `/usr/share/calendar` 中。下表给出了每个日历文件的名称并描述了其内容。

| 日历文件 | 描述 |
|---|---|
| calendar.birthday | 名人的出生和死亡。 |
| calendar.christian | 基督教节日。 |
| calendar.computer | 计算历史上的重要日期。 |
| calendar.history | 美国历史事件的日期。 |
| calendar.holiday | 标准和冷门的假日。 |
| calendar.judaic | 犹太教节日。 |
| calendar.music | 与音乐相关的日期，主要是 1960 年代的摇滚乐。 |
| calendar.usholiday | 美国假日。 |
| calendar.hindu | 印度教节日。 |

要让 `calendar` 在输出你的常规预约时同时输出其中一个文件中的日期，请在你的日历文件中加入以下内容，其中 *file* 是你想要包含的特定日历文件的名称：

```
#include <file>
```

例如，要在运行 calendar 时同时输出美国假日和著名出生与死亡，请在你的日历文件中加入以下几行：

```
#include <calendar.usholiday>
#include <calendar.birthday>
```

注意：当然，你可以将自己的日历文件与其他用户共享；这对于为团体或组织制作特殊日历很有用。如果日历文件在当前目录或 `/usr/share/calendar` 中，你只需给出文件名；否则，在包含语句中给出其完整路径名。

## 28.4.3 自动预约交付

你可以自动化你的预约服务，以便每次登录或启动新 shell 时都会交付你的预约和提醒，或者你可以让当天的提醒每天早上通过电子邮件发送给你。

将 calendar 添加到你的 `.bashrc` 文件中，以便每次登录或启动新 shell 时输出当天的预约和提醒（请参阅“自定义未来 Shell”部分）。

如果你将日历文件保存在主目录以外的目录中，请确保 calendar（该工具）是从该目录调用的。例如，如果你的日历文件在你的 `~/doc/etc` 目录中，你将在 `.bashrc` 文件中加入以下行：

```
cd ~/doc/etc; calendar; cd
```

要让系统通过电子邮件向你发送当天的预约，请使用 crontab 安排一个每天运行的 cron 作业进程，该进程运行 calendar 并在有输出时通过 mail 将其发送给你。

