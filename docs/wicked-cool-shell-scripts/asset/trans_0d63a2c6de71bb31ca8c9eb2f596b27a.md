

## Hacking the Script

知道世界各地特定时区的时间是一项很棒的能力，尤其是对于管理全球网络的系统管理员来说。但有时，你只是想快速知道两个时区之间的时间差。timein 脚本可以被修改来提供这一功能。通过基于 timein 脚本创建一个新脚本，或许命名为 tzdiff，你可以接受两个参数而不是一个。

利用这两个参数，你可以确定两个时区的当前时间，然后打印出两者之间的小时差。需要注意的是，两个时区之间的两小时差异可能是向前两小时，也可能是向后两小时，这差别很大。区分两小时差异是向前还是向后，对于使这个 hack 成为一个有用的脚本至关重要。

## 3

## CREATING UTILITIES

![](img/4ffb1cc24a1b24b49254839643abedb2_110_0.png)

创建 shell 脚本的主要目的之一是将复杂的命令行序列写入文件，使其可重复且易于调整。因此，本书中用户命令遍布其中也就不足为奇了。令人惊讶的是什么？我们还没有为 Linux、Solaris 和 OS X 系统上的每个命令都编写一个包装器。

Linux/Unix 是唯一一个主要操作系统，你可以在其中决定自己不喜欢某个命令的默认标志，并用几个击键永久修复它，或者你可以通过别名或十几行脚本来模拟来自其他操作系统的你最喜欢的实用程序的行为。这就是 Unix 如此极具乐趣的原因——也是写这本书的初衷！

### #22 A Reminder Utility

Windows 和 Mac 用户多年来一直欣赏像 Stickies 这样简单的实用程序，这些精简的应用让你可以在屏幕上保留微小的便笺和提醒。它们非常适合记下电话号码或其他提醒。不幸的是，如果你想在 Unix 命令行上做笔记，就没有类似的东西，但这个问题很容易通过这对脚本解决。

第一个脚本 remember（见清单 3-1），让你可以轻松地将信息片段保存到你主目录中的单个 rememberfile 中。如果不带任何参数调用，它会读取标准输入，直到给出文件结束序列（^D），即按 CTRL-D。如果带参数调用，它就直接将这些参数保存到数据文件。

这对脚本的另一半是 remindme，一个伴随的 shell 脚本，见清单 3-2，它在没有参数给出时显示整个 rememberfile 的内容，或者使用参数作为模式在其中搜索并显示结果。

### The Code

```
#!/bin/bash

# remember--An easy command line-based reminder pad

rememberfile="$HOME/.remember"

if [ $# -eq 0 ] ; then
    # Prompt the user for input and append whatever they write to
    # the rememberfile.
    echo "Enter note, end with ^D: "
    cat - >> $rememberfile
else
    # Append any arguments passed to the script on to the .remember file.
    echo "$@" >> $rememberfile
fi

exit 0
```

清单 3-1：The remember shell script

清单 3-2 详细说明了伴随脚本 remindme。

```
#!/bin/bash

# remindme--Searches a data file for matching lines or, if no
# argument is specified, shows the entire contents of the data file

rememberfile="$HOME/.remember"

if [ ! -f $rememberfile ] ; then
    echo "So: You don't seem to have a .remember file." >&2
    echo "To remedy this, please use 'remember' to add reminders" >&2
```

```
exit 1
fi

if [ $# -eq 0 ] ; then
# Display the whole rememberfile when not given any search criteria.
more $rememberfile
else
# Otherwise, search through the file for the given terms, and display
# the results neatly.
grep -i -- "$@" $rememberfile | ${PAGER:-more}
fi

exit 0
```

清单 3-2：The remindme shell script, a companion to the remember shell script in Listing 3-1

### How It Works

清单 3-1 中的 remember shell 脚本可以作为交互式程序工作，要求用户输入要记住的详细信息，或者它也可以被脚本化，因为它也可以简单地将任何内容作为命令行参数接受。如果用户没有向脚本传递任何参数，我们会做一些巧妙的编码。在打印出如何输入条目的用户友好消息后，我们使用 cat ① 从用户读取数据：

```
cat - >> $rememberfile
```

在之前的章节中，我们使用 read 命令从用户获取输入。这行代码使用 cat 从 stdin 读取（命令中的 - 是 stdin 或 stdout 的简写，具体取决于上下文），直到用户按下 CTRL-D，这告诉 cat 实用程序文件已结束。随着 cat 打印它从 stdin 读取的数据，并将此数据附加到 rememberfile。

如果向脚本指定了参数，则所有参数都将原样附加到 rememberfile ②。

清单 3-2 中的 remindme 脚本如果 rememberfile 不存在就无法工作，因此我们在尝试做任何事情之前先检查 rememberfile 是否存在。如果 rememberfile 不存在，我们在打印一条消息提醒用户原因后立即退出。

如果没有向脚本传递参数，我们假设用户只是想查看 rememberfile 的内容。使用 more 实用程序允许分页浏览 rememberfile，我们只需将内容显示给用户 ③。

否则，如果向脚本传递了参数，我们将执行不区分大小写的 grep 搜索 rememberfile 中任何匹配的术语，然后也分页显示这些结果 ④。

### Running the Script

要使用 remindme 实用程序，首先使用 remember 脚本向 rememberfile 添加笔记、电话号码或其他任何内容，如清单 3-3 所示。然后使用 remindme 搜索这个自由形式的数据库，指定你想要的任意长或短的模式。

