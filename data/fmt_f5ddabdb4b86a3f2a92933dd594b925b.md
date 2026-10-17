
printer long_queue disabled since Tue May 7 07:02:01 EDT 2007. available.

stopped by user

printer s_q_nam disabled since Tue May 7 07:02:01 EDT 2007. available.

stopped by user

printer hp4 unknown state. enabled since May 07 07:30 2007. available.

printer yogi_hp4_lps unknown state. enabled since May 07 07:30 2007. available.

# 列表 25-5 `lpstat -a` 和 `lpstat -p` 输出

注意列表 25-5，每个命令选项在输出的每行中都为每台打印机提供了一组独特的状态信息。我们希望利用状态的唯一性作为 `grep` 语句中的标签。这些术语也是合理的。队列要么接受新请求，要么不接受新请求，而打印机要么已启用打印，要么已禁用了打印。由于我们只对“已禁用”和“不接受”的状态感兴趣，我们可以创建一个简单的脚本或单行命令。

为了启用打印并恢复打印队列接受新请求，我们需要知道两件事：打印机/队列名称以及队列或打印机状态。第一步过滤出包含我们标签的输出行。第二步是从每行输出中提取打印机/队列名称。让我们先看看使用 `while` 循环来启动所有项目，如列表 25-6所示。

```bash
lpstat -a | grep 'not accepting' | while LINE
do
  Q=$(echo $LINE | awk '{print $1}')
  lpc enable $Q
done

lpstat -p | grep disabled | while LINE
do
  P=$(echo $LINE | awk '{print $2}')
  lpc start $P
done
```

# 列表 25-6 使用 `-a` 和 `-p` 编写 `lpstat` 命令

注意列表 25-6，我们必须通过两个独立的循环分别处理打印队列和打印机。在第一个 `while` 循环中，启动了所有的队列功能。在第二个循环中，我们启用了每台打印机的打印功能。这种方法的缺点是，当你有数百台打印机时，可能花费很长时间；如果你有数百台打印机，应该使用 `lpc all` 一次性启动所有项目。

正如我之前提到的，我们也可以将列表 25-6 中的两个循环变成单行命令。我们可以在同一行中组合 `grep` 和 `awk` 命令，并使用命令替换来执行 `lpc` 命令。以下两个循环替换了原来的两个循环：

```bash
lpc enable $(lpcstat -a | grep 'not accepting ' | awk '{print $1}')
```

```bash
lpc start $(lpcstat -p | grep disabled | awk '{print $2}')
```

第一条命令启用队列功能，第二条命令启动打印。命令替换使用 `$ (command)` 语法，在标签上执行相应的 `lpcstat` 命令并提取打印机/队列名称。生成的输出被用 `lpc` 命令的参数。

# CUPS – 通用 UNIX 打印系统

以下语句来自 www.cups.org：

> CUPS 为基于 UNIX 的操作系统提供了一个可移植的打印层。它最初由 Easy Software Products 开发，现在由 Apple Inc. 拥有并维护，以推广标准的打印解决方案。它是 Mac OS X 和大多数 Linux 发行版中的标准打印系统。

CUPS 使用互联网打印协议（"IPP"）作为管理打印作业和队列的基础，并添加了基于 PostScript 打印机描述（"PPD"）的打印选项以支持现实世界的打印。

我在我的 Fedora 7x64 系统 booboo 上使用 CUPS。如果你不熟悉 CUPS，查看此处 URL 中的手册将是个好主意：

```
http://www.cups.org/doc-1.1/sum.html
```

在 CUPS 中打印文档时，你拥有的控制能力是惊人的。打印选项的细节超出了本书的范围，让我们来看看如何控制打印和队列。

CUPS 使用 BSD 命令 `lpc` 来查看队列状态，控制打印和队列是通过表 25-3 所示的命令完成的。

我们对恢复队列和打印感兴趣，因此 `accept` 和 `cupsenable` 是我们用于启动已队列作业以及接受新打印作业进入队列的命令。我们只需要检查队列状态并重新启用任何处于关闭状态的项目。

# 表 25-3 CUPS 命令表

| CUPS 命令 | 命令结果 |
| :--- | :--- |
| accept | 开始打印队列中的作业 |
| reject | 停止打印队列中的作业 |
| cupsenable | 允许新的打印作业 |
| cupsdisable | 拒绝新的打印作业 |

警告信息告诉我们打印机已宕；然而，请注意队列状态并没有列出。现在让我们关闭 hp4_yogi_1 打印队列，看看会发生什么：

```
# reject hp4_yogi_1
destination "hp4_yogi_1" will no longer accept requests
```

使用 `lpstat -a` 命令仅查看排队状态，如下所示：

```
# lpstat -a
hp4_yogi_1 not accepting requests since Oct 1 05:45 -
  reason unknown
yogi_hp4_lps accepting requests Sep 26 04:23
```

由于 hp4_yogi_1 现在禁用了打印并停止了排队，我预计我们第一次会在 `lpstat` 命令的输出中看到一些队列状态的输出：

```
# lpstat
printer queue for hp4_yogi_1
dino: Warning: hp4_yogi_1 queue is turned off
dino: Warning: hp4_yogi_1 is down
printer queue for yogi_hp4_lps
```

正如我们预期的那样。通过这个小练习，我们了解到，只有当使用 `lpstat` 命令行停止队列上的排队时，才会报告排队状态。为了实现我们的效果，让我们使用 `lpstat` 的输出。我们想用 "Warning" 一词作为 `grep` 语句的标签。然后我们可以 `grep` 提取出的这一行来检查打印和排队状态。如果存在字符串 'queue is turned off'我们就知道排队已关闭；如果行中出现字符串 'is down'我们就知道打印已禁用。剩下的唯一工作是提取打印机/队列名称，它始终位于第三字段。

要编写此脚本，我们可以使用列表 25-9 中的代码。请注意**粗体**类型，我们将在最后介绍该脚本。

```
#!/bin/ksh
#
# SCRIPT: print_UP_HP-UX.ksh
#
## AUTHOR: Randy Michael
# DATE: 03/14/2007
# REV: 1.1.P
#
```

**Listing 25-9** `print_UP_HP-UX.ksh` shell 脚本

```
# PLATFORM: HP-UX Only
#
# PURPOSE: 此脚本用于分别启用 HP-UX 系统上
# 每个打印队列的打印和排队。
#
## REV LIST:
#
# set -x # 取消注释以调试此脚本
# set -n # 取消注释以不执行检查语法
lpstat | grep | while read LINE
do
    if $(echo $LINE | grep 'is down') > /dev/null
    then
        enable $(echo $LINE | awk '{print $3}')
    fi
    if $(echo $LINE | grep 'queue is turned off') >/dev/null
    then
        accept $(echo $LINE | awk '{print $3}')
    fi
done
```
