
```
$ cal 06 1991 RET

June 1991

S M Tu W F S 1

2 3 4 5 6 7 8

9 10 11 12 13 14 15

16 17 18 19 20 21 22

23 24 25 26 27 28 29

30

$
```

## 27.3.2 在 Emacs 中显示日历

Emacs 自带日历服务。`calendar`函数会在新缓冲区中显示为期三个月的日历——它会显示当前月、上个月和下个月，并将光标（point）置于当前日期上。要选择要显示的月份和年份，可以在`calendar`命令前加上通用参数命令`C-u`。

- 在 Emacs 中，要显示当前月份和年份的三月日历，输入：
  `$ M-x calendar`
- 在 Emacs 中，要显示 2010 年 8 月的三月日历，输入：
  `C-u M-x calendar`
  `Year (>0): 2001 BKSP BKSP 10 RET`
  `Month name: Aug RET`

> 注意：在显示特定月份和年份的日历时（如上例），当前年份为 2001，输入两次`BKSP`以删除最后两位数字，然后将其替换为“10”，从而使其变为 2010 年。

## 27.4 管理安排

Debian: `bsdmainutils`

`calendar`工具是一个提醒服务，你可以用它来管理安排。它读取一个日历文件，该文件是当前目录下的文本文件，包含安排和提醒列表；然后它输出文件中日期为今天或明天的条目。（如果是周五，它会输出该周末以及下周一的条目。）

例如，如果今天是 6 月 16 日周五，且你在与日历文件相同的目录下运行`calendar`，典型的输出如下：

```
$ calendar RET

6/16    Finish draft of book

        Party at Jack's

Fri     Lunch with Kim and Jo, 12:30

Mon     Book manuscript due

$
```

据报道，`calendar`工具首次出现在 AT&T UNIX 第 7 版本中，并早期为 BSD Unix 家族重写。虽然 BSD 派生版本作为`bsdmutils`包的一部分提供给 Debian，但该工具并不是所有 Linux 发行版中的标准配置。

以下是编写日历文件的食谱，包括在你的自己的日历文件中包含其他日历文件，以及自动发送提醒的方法。

> **注意：** Emacs 有一个与此工具等效的功能，称为“Diary”（日记）。请参阅 Info 文件‘emacs-e20.info’中的注释‘Diary’以获取有关该功能的更多信息。

### 27.4.1 创建安排文件

要开始使用`calendar`，你需要创建一个“日历文件”，并在其中输入你的安排。它只是一个纯文本文件，可以命名为`calendar`或`.calendar`；后者会使其成为“隐藏”文件，正如食谱 5.3.4 [列出隐藏文件] 第 73 页所述。

将每个安排或日历条目单独写一行；文件中的空行会被忽略。日历条目的的格式如下：

```
[日期 | 制表符或空格] [提醒内容本身]
```

几乎所有常见的日期格式都能被识别。例如，以下都是7 月 4 日的有效日期：

```
7/4

July 4

July 4

Jul. 4

Jul 4
```

条目并不限于某一天；你可以为每周的某一天或特定月份设置条目，例如‘Mon’或‘Monday’代表每个周一；‘Jun’或‘June’代表每个 6 月的第一天。你也可以使用星号：`/*13*`会提醒你每个月的 13 号有某事。当某行省略日期时，则假设为上一个安排的日期。

例如，假设你的家目录下有一个名为`calendar`的文件，内容如下：

```
6/16    Finish draft of book

        Party at Jack's

6/20    Gallery reading

Fri     Lunch with Kim and Jo, 12:30

Mon     Book manuscript due
```

如果当前是 6 月 16 日周五，且你在家目录下运行`calendar`，你将得到与上一节节食谱 27.4 [管理安排] 第 288 页示例相同的输出。

### 27.4.2 在提醒中包含节日

注意：在上面的示例中，派对的条目没有日期——它使用了上一个条目的日期‘6/16’。

`calendar`软件包包含了一系列针对各种节日和其他场合的准备日历文件，你可以在自己的日历文件中引用这些文件，以便将它们的条目包含在你自己的提醒中。

准备文件存储在`/usr/share/calendar`中。下表列出了每个日历文件的名称并描述了其内容。

| CALENDAR FILE | DESCRIPTION |
|---|---|
| calendar.birthday | 名人的出生去世。 |
| calendar.christian | 基督教节日。 |
| calendar.computer | 计算机节。 |
| calendar.history | 历史事件。 |
| calendar.holiday | 普通节日。 |
| calendar.music | 音乐节。 |
| calendar.juda | 犹太节。 |
| calendar.hindu | 印度教节。 |

要让系统输出你的安排，请在文件中放入以下内容：

```
#include <calendar>
```

# Linux 菜谱：日常使用的技巧与技术

John Dos Passos
1919 America Ave.
纽约市

###

Scott F. - 602 555 1803
(请在 12 点后拨打)

###

T. Wolfe 的新邮箱已更改。
新邮箱是：tw@example.com

注意，每个条目都包含各种信息，且没有特定的格式。这就是自由格式列表的优势——你不需要按照特定顺序输入条目，也不受限于一组特定的“字段”；你甚至可以将文本剪切粘贴到邮件、网页或其他窗口中（参见菜谱 10.4 [选择文本]，第 128 页）。

有几种方法可以找到这样的文件。例如，假设你想联系朋友 Scott，需要他的电话号码。

- 输出输出文件中包含文本 'scott' 的行，且不区分大小写：

```
$ grep -i scott rolo

Scott F. - 602 555 1803

$ 
```

当你需要的信息与搜索的信息在同一行时，这种方法非常有效——在这里，名字 Scott 与电话号码在同一行；然而，输出并没有显示文件中下一行出现的警告。如果你要搜索的术语和你需要的信息在相邻的行怎么办？

使用`grep`的 '-C' 选项可以输出匹配行前后的几行上下文。

- 输出匹配文本 'olfe' 的行周围的几行，输入：

```
$ grep -C olfe rolo

T. Wolfe's new email has changed.

The new one is: tw@example.com

$ 
```
