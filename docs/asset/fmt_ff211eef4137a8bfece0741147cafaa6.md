
此示例显示可以为用户 `jake` 在 `/dev/hda2` 分区上设置用户配额（在我们的示例中为 `/home`）。目前，`jake` 已使用 596 个块（在 ext3 文件系统中，一个块等于 1K）。`jake` 创建了一个文件（用 1 个 inode 表示）。要更改磁盘限制，你可以编辑 `soft` 和 `hard` 标题下的 `0`（表示无限制使用）。

`soft` and `hard` inodes `soft` `hard`
(a block equals 1K on the ext3 file system). One file was created by `jake` (represented by 1 inode). To change the disk limits, you can edit the zeros (unlimited use)

## 第三部分：管理配额

## 删除临时文件

某些潜在的磁盘空间问题会自动处理。例如，应用程序使用的目录（如 `/tmp` 和 `/var/tmp`）随着时间的推移会大量空间。为了解决这个问题，Fedora 提供了 `tmp` 机制。`tmpwatch` 命令从 `cron.daily/tmp` 运行以删除未使用的文件。以下是该文件的内容：

```bash
/usr/sbin/tmpwatch 240 /tmp

/usr/sbin/tmpwatch 720 /var/tmp

for d in /var/{cache,catman}@{X11?,local/cat?}; do

  if [ -d "$d" ]; then

    /usr/sbin/tmpwatch -f 720 $d

  fi

done
```

每天，此 `tmpwatch` 脚本运行以删除一段时间未使用的文件。来自 `/tmp` 和 `/var/tmp` 目录的文件在未访问 240 和 720 小时后删除。存储在 `/var/cache` 子目录中的临时页面也会在 720 小时后检查并删除。

## 更新设置

更改配额后，你应该重新运行 `quota` 检查配额。

要报告每个用户使用了多少磁盘空间，使用 `repquota` 命令。以下是所有分区的示例：

```bash
# repquota -a
```

## 使用 du 检查磁盘使用情况

你可以使用 `du` 发现最大的磁盘使用者。`-h` 选项以字节（k）、兆字节（M）或千字节（G）显示数字。`-c` 选项添加所有目录的总和。

```
339M /home/tom
81M /home/bill
31M /home/tina
44k /home/sally
450M total
```

有时你需要向系统上的所有用户发送消息。警告用户由于硬件升级导致的计划停机是一个很好的例子。单独向每个用户发送电子邮件极其耗时且浪费；这正是邮件别名和邮件列表设计的初衷。维护一个当前所有用户的邮件列表，随着你添加和删除用户，它变得越来越不准确。此外，如果你的系统有很多用户，别名列表的大小可能会变得难以管理。

下面的脚本名为 `mailfile`，提供解决这些问题的简单方法。它从 `/etc/passwd` 文件中获取登录名并向所有用户发送电子邮件。

```bash
#!/bin/ksh
```

# 434 第三部分：管理 Fedora

```bash
# mailfile: 此脚本将指定的文件通过发送给系统所有用户。
# 它会跳过前 17 个账户，以便
# 我们不会将邮件发送给如 'root' 这样的系统账户。
# 用法：mailfile "此处输入主题" filename.txt
#
# 检查是否存在主题
#
if ( `echo $1 | awk '{ print $1 }' == "" ) then
    echo 您没有为消息提供主题。
    echo 请务必将其包含在引号中。
    exit 1
else
    # 获取消息的主题
    set subject=$1
endif
#
# 检查是否存在文件名
#
if ( $2 == "" ) then
    echo 您没有提供文件名。
    exit 2
else
    # 获取要发送的文件名
    set filename=$2
endif
#
# 检查文件是否存在
#
if ( -f $filename ) then
    echo 正在发送文件 $filename
else
    echo 文件不存在。
    exit 3
endif
#
# 遍历每个登录名，但跳过前 17 个账户
#
foreach user (`awk -F: '{ print $1 }' /etc/passwd | tail +17`); do
    # 发送邮件
    echo 正在向 $user 发送邮件
    mail -s "$subject" $user < $filename
```

# 第11章：设置与支持用户 435

```bash
# 睡眠几秒，以免让邮件发送程序过载
# 在账户较少的快速系统中，
# 你可能可以去掉这个延迟。
sleep 2
```

该脚本接受两个参数。第一个是电子邮件消息的主题，包含在引号中。第二个是包含要发送的文本消息的文件名。因此，为了向所有用户发送电子邮件，警告他们即将到来的服务器硬件升级，你可以执行类似下面的操作：

```bash
mailfile "系统将于下午 5:00 升级" upgrade.txt
```

`upgrade.txt` 文件包含了要发送给每个用户的消息文本。这种方法真正有用的地方在于，我可以保存这个文本文件，并在下次升级系统时轻松地修改并重新发送。

> 提示：如果你的用户使用基于文本的登录而不是图形界面登录到你的系统，你可以向 `/etc/mot.d` 文件添加消息，让它们到达你的用户。该文件中的任何文本都将在用户登录后、第一个 shell 提示符出现之前显示在用户的屏幕上。

## 总结

Linux 系统作为没有实际用户的单任务服务器并不罕见。它静静地坐在服务器机里，提供 Web 页面或处理域名服务，从不崩溃，很少需要关注。然而，情况并非总是如此。你可能需要支持 Linux 系统上的用户，而这可能是系统管理工作中最具挑战性的部分。

Fedora 提供了各种工具来帮助你完成管理工作。`useradd`、`usermod` 和 `usdel` 命令允许通过命令行操作用户账户数据。此外，创建一个支持性邮件邮箱箱并构建 shell 脚本来自动化重复任务可以进一步减轻你的负担。Fedora Linux 构建在丰富的 UNIX 历史之上，提供了一个理想的平台来支持你用户的多样化需求。

# 第12章

## 自动化系统任务

本章内容

- 理解 shell 脚本
- 系统初始化
- 系统启动与关闭
- 调度系统任务

如果你在系统启动时手动输入每个需要运行的命令，你将无法完成任何工作。同样，如果你将经常运行的一组命令组合在一起，你的工作会更高效。`shell` 脚本可以处理这些任务。

`shell` 脚本是一组命令、函数、变量或几乎你在 shell 中使用的任何其他内容。这些项目被输入到一个纯文本文件中。该文件随后可以作为命令运行。Fedora 在系统启动期间使用系统初始化 shell 脚本来运行启动系统所需的命令。你可以创建自己的 shell 脚本来自动化你经常需要执行的任务。

本章对 shell 脚本的内部原理及其用法提供了简要的概述。你将学习 shell 脚本是如何负责系统引导的，以及如何将简单的脚本用于调度设施（如 `cron` 或 `at`）来简化管理任务。

你还学习了如何调优你的机器使其在最合适的时间启动并仅运行你需要的服务。有了这些理解，你将能够个性化你的计算机，并减少重复输入相同命令花费的时间。

## 理解 shell 脚本

你是否有过一个需要重复执行且在命令行中需要大量键的任务？你是否曾想过：“哇，我希望只要输入一个命令就能完成这一切？”也许 shell 脚本正是你所寻找的。

`shell` 脚本相当于 MS-DOS 中的批处理，可以包含长命令列表、复杂的流程控制、算术求值、用户定义变量、用户定义函数和复杂的条件测试。`shell` 脚本能够处理从简单的单行命令到启动 Fedora 系统等复杂的任何任务。

事实上，正如你在本章中所读到的，Fedora 正是那样做的。它使用 shell 脚本 `/etc/rc.d/rc.sysint` 来检查并挂载所有文件系统，设置控制台，配置网络，启动所有系统服务，并最终为你提供登录界面。虽然 Fedora 中提供了近十种不同的 shell，但默认 shell 是 `bash`。

`shell` 脚本相当于 MS-DOS 中的批处理，可以包含长命令列表、复杂的流程控制、算术求值、用户定义变量、用户定义函数和复杂的条件测试。`shell` 脚本能够处理从简单的单行命令到启动你的 Fedora 系统等复杂的任何任务。

事实上，正如你在本章中所读到的，Fedora 正是那样做的。它使用 shell 脚本 `/etc/rc.d/rc.sysint` 来检查并挂载所有文件系统，设置你的控制台，配置网络，启动所有系统服务，并最终为你提供登录界面。虽然 Fedora 中提供了近十种不同的 shell，但默认 shell 是 `bash`。

# 440 第三部分：管理 Fedora

位置参数 `$0` 将是 `myscript`，`$1` 将是 `foo`，而 `$2` 将是 `bar`。另一个变量 `$#` 存储了你的脚本接收了多少参数。在我们的示例中，另一个特别有用的特殊变量是 `$?`，它接收上一次执行命令的退出状态。通常，值 `0` 表示一切正常，任何非 `0` 值都表示某种类型的错误。有关特殊变量的完整列表，请参考 `bash` man 页面。

## bash 中的参数扩展

如前所述，如果你想获取变量的值，请在变量前面加上一个 `$`（例如 `$CITY`）。这实际上是符号 `${CITY}` 的简写；当参数值需要紧挨在一起而没有空格时，就会使用大括号。Bash 有特殊的规则，允许你以不同的方式扩展变量的值。对于对 shell 脚本的快速介绍来说，介绍所有的规则可能有点大过其实，但表 12-1 展示了一些你可能在 Fedora 设备找到的 bash 脚本中看到的常见结构。

## 表 12-1：bash 参数扩展示例

| 结构 | 含义 |
| --- | --- |
| `${var:-value}` | 如果变量未设置或为空，则将其扩展为 value |
| `${var*pattern}` | 从 var 值的结尾删除与 *pattern* 匹配的最短 |
| `${var##pattern}` | 从 var 值的结尾删除与 *pattern* 匹配的最长部分 |
| `${var%%pattern}` | 从 var 值的开头删除与 *pattern* 匹配的最短 |
| `${var##pattern}` | 从 var 值的开头删除与 *pattern* 匹配的最长部分 |

```
尝试在 shell 中运行以下命令来测试参数扩展是如何运作的：

# THIS="Example"
# THIS=${THIS:-"Not Set"}
# THAT=${THAT:-"Not Set"}
echo $THIS
Example
echo $THAT
Not Set.
```

在之前的示例中，变量 `THIS` 被设置为单词 `Example`。在接下来的两行中，变量 `THIS` 和 `THAT` 变量分别被设置为它们当前的值，或者在它们当前未设置时设置为 `Not Set`。请注意，由于我们刚刚将 `THIS` 设置为字符串 `Example`，当我们 `echo THIS` 的值时，它显示为 `Example`。然而，由于 `THAT` 没有设置，它显示为 `Not Set`。

# 第 12 章：自动化系统任务

> 注意：在本节的剩余部分，我将展示变量和命令可能出现在 shell 脚本中。但是，要尝试任何这些示例，只需像上一个示例那样将它们输入 shell 即可。

在下面的示例中，设置 `MYFILENAME=/home/digby/myfile.txt`。接下来，将 `FILE` 变量设置为 `myfile.txt`，并将 `DIR` 设置为 `/home/digby`。在 `NAME` 变量中，文件名被简化为 `myfile`，然后在 `EXTENSION` 变量中将扩展名设置为 `txt`。（要尝试这些，你可以像上一个示例一样在 shell 提示符处输入它们，然后 `echo` 每个变量的值以查看它是怎样的。）

```
MYFILENAME="home/digby/myfile.txt"
FILE=${MYFILENAME##*/} # FILE 变成 "myfile.txt"
DIR=${MYFILENAME%*/} # DIR 变成 "/home/digby"
NAME=${FILE%.*} # NAME 变成 "myfile"
EXTENSION=${FILE##.} # EXTENSION 变成 "txt"
```
