
# swap -s

total: 26788k bytes allocated + 7256k reserved = 34044k used, 557044k available

```
这是一个不寻常的输出，因为数据都在同一行，但由于 Solaris 试图创建一个数学等式，我们必须使用自己的数学表达式来填充空白，以获得所需的脚本输出。`swap` 命令输出显示系统总共有 34MB 和 557MB 的可用空间。我们必须计算总 MB、使用百分比和交换空间的剩余百分比。这些计算...

## 创建 Shell 脚本

现在我们有了数据，可以开始编写脚本了。

## 监控分页与交换空间 151

关于可用分页空间的百分比，我们需要从 100 中减去使用的百分比值，如下面的语句所示。

```
(( PAGING_PC_FREE = 100 - PAGING_PC ))
```

注意，我们使用了双括号数学方法，它由 `(( Math Statement ))` 指定。我喜欢这种方法，因为它用起来很直观。还要注意，在使用这种方法时，变量不需要使用美元符号 `$`。因为双括号期望的是一个数学语句，任何非数字字符都会被假设为变量，因此应该省略美元符号。如果你在变量名中添加了美元符号，该语句可能会根据你运行的操作系统而失败！我总是会去掉美元符号，以防万一。这是使用 shell 脚本时常见的令人挫败的原因，而且极难排错。

下一个计算对某些人来说并不直观。我们想要计算当前使用的分页空间大小（MB）。现在让我们谈谈这个。我们有分页空间的百分比、可用分页空间的百分比以及以 MB 为单位的总分页空间。为了计算已分页空间的 MB 以及将分页空间百分比除以 100（这几乎将已分页空间的值转换为十进制值），看看下一个语句是如何操作的。

```
(( MB_USED = PAGING_MB * PAGING_PC / 100 ))
```

关于最后一条语句需要考虑的一点：这将只会产生整数输出。如果你想以浮点表示法输出，则需要使用 `bc` 工具，你将在接下来的某个章节中看到它。

最后一个计算不是另一个直观的计算，而是寻找可用分页空间的 MB。因为我们已经有了以 MB 为单位的总分页空间值以及正在使用的分页空间 MB，所以我们需要从总值中减去使用值。如下面的语句所示。

```
(( MB_FREE = PAGING_MB - MB_USED ))
```

我们已经完成了所有的计算，现在准备好为 axis shell 脚本准备所需的输出。查看列表 6.3 中显示的整个 shell 脚本，并特别注意**粗体类型**。

```bash
#!/usr/bin/ksh

#

# 脚本:AI_paging_mon.ksh

#

## 作者: Randy Michael

# 日期:5/31/2002

# 版本:1.1.P

#
```

**列表 6.3** `AI_paging_mon.ksh` shell 脚本列表。（继续）

## 152 第 6 章

```bash
# 平台：仅限X

#

# 目的：此 shell 脚本用于生成系统分页空间统计报告，

# 包括：

#

# 以 MB 为单位的总分页空间、可用分页空间 MB、

# 使用分页空间 MB、分页空间使用百分比以及

# 分页空间可用百分比

#

# 版本列表:

#

# set -x 取消注释以调试此 shell 脚本

# set -n 取消注释以在不执行的情况下检查命令语法
############################################################
################# 在处定义变量 #################
PC_LIMIT=65      # 分页空间百分比上限

                  # 通知前的阈值

THISHOST=$(hostname)  # 此机器的主机名
PAGING_STAT=/tmp/paging_stat # 分页统计文件
############################################################
################# 初始化报告 #################
echo "\nPaging Space Report for $THISHOST\n"
date
############################################################
################# 捕获并处理数据 #################
# 加载不带列标题的文件
lps -s | tail +2 $PAGING_STAT
# 开始一个 while 循环并使用 $PAGING_STAT 文件作为# 重定向输入从底部引导循环，在 "done" 之后
while read TOTAL PERCENT
do
  # 通过移除后缀清理数据
  PAGING_MB=$($TOTAL | cut -d 'MB' -f1)
  PAGING_PC=$($PERCENT | cut -d%' -f1)
  # 计算缺失的数据：可用百分%、已用 MB 和可用 MB
  (( PAGING_PC_FREE = 100 - $PAGING_PC ))
```

列表 6.3 `AIX_paging_mon.ksh` shell 脚本列表。（继续）

## 监控分页与交换空间 153

```bash
(( MB_USED = PAGING_MB * PAGING_PC / 100 ))
(( MB_FREE = PAGING_MB - MB_USED ))
# 生成剩余的分页空间报告：
echo "\nTotal MB of Paging Space:\t$TOTAL"MB"
echo "Total MB of Paging Space Used:\t$(MB_USED)"MB"
echo "Total MB of Paging Space Free:\t$(MB_FREE)"MB"
echo "\nPercent of Paging Space Used:\t$(PERCENT)%"
echo "\nPercent of Paging Space Free:\t$(PAGING_PC_FREE)%"
# 检查分页空间是否超过预定义的限制
if (( PC_LIMIT <= PAGING_PC ))
then
    分页空间超过限制，发送通知
    tput smso # 开启反色视频！
    echo "\n\nWARNING: Paging Space has Exceeded the ${PC_LIMIT}% \
Upper Limit!\n"
    tput rmso # 关闭反色视频
fi
done < $PAGING_STAT
rm -f $PAGING_STAT
# 在输出中添加额外的换行
echo "\n"
```

**列表 6.3** `AIX_paging_mon.ksh` 脚本列表。（继续）

列表 6.3 中我们的 shell 脚本有一部分我们还没有涵盖。在脚本顶部定义变量的地方，我添加了 `PC_LIMIT` 变量。我通常将其设置为 65%，这样我就会知道何时超过了安全的系统分页限制。当你的系统开始在高分页水平运行时，你需要找到导致这种额外活动的原因。有时开发者在释放内存时写得不正确。如果一个程序运行很长时间，且没有编写为清理和重用分配的内存，则称该程序存在内存泄漏。这种内存泄漏程序在长时间运行而不重启系统的情况下，结果是你的系统将耗尽内存。当你的系统内存耗尽时，它开始在磁盘上进行分页交换，然后你的分页开始上升。大多数情况下，解决此问题并恢复内存的唯一方法是重启系统。

## 第 6 章

注意脚本末尾有一个测试，检查分页空间使用百分比是否大于等于 `PC_LIMIT` 变量设置的限制。如果超过了该值，将开启反色视频，使 **WARNING** 消息在屏幕上显目。当消息显示时，反色视频会被关闭。要开启反色视频使用 `tput smso` 命令。当反色视频开启时，你打印的任何内容都会以反色视频显示；但是，不要忘记关闭此模式否则它在脚本执行结束后仍会继续。关闭反色视频模式使用 `tput rmso` 命令。列表 6.4 和 6.5 显示了脚本的运行情况。列表 6.4 显示了在限制内的报告，而列表 6.5 显示了系统超过 65% 限制时的报告。

```
Paging Space Report for yogi

Fri Jun 7 15:47:08 2002

Total MB of Paging Space: 336MB

Total MB of Paging Space Used: 6MB

Total MB of Paging Space Free: 330MB

Percent of Paging Space Used: 2%

Percent of Paging Space Free: 98%
```
