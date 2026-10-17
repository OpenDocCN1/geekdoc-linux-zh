
echo "\nPercent of Swap Used:\t($PERCENT_USED)%"

echo "\nPercent of Swap Free:\t($PERCENT_FREE)%%"

# 获取使用百分比的整数部分

```bash
INT_PERCENT_USED=$(echo $PERCENT_USED | cut -d. -f1)
```

# 检查是否超过了使用百分比的最大阈值

```bash
if (( PC_LIMIT <= INT_PERCENT_USED ))
then
# 百比已超过阈值，发送通知
tput smso # 开启反色显示！
```

列表 18-14（续）

# 第 18 章 监控分页与交换空间 629

```bash
echo "\nWARNING: Swap Space has Exceeded the ${PC_LIMIT}% \
Upper Limit!\n"
tput rsmso # 关闭反色显示！
fi
echo "\n"
```

列表 18-14（续）

注意我们是如何通过两次读取 `swap -s` 命令的输出使用了两个 `awk` 语句的。这两个测量值发生的时间非常短，所以应该没有影响；然而，你可能想将方法更改为单次读取并将输出存储在变量或文件中。我将这个修改任务留给你们作为练习。在下一步中，我们将空闲交换空间的 KB 加上到已用交换空间的 KB 之上，以找到系统上的总交换空间。

通过这三个 KB 值，我们使用命令替换语句内部的 `bc` 工具来计算空闲和使用空间的百分比，同时使用文档为 `bc` 命令提供输入。在准备打印之前还有最后一步——将 KB 转换为 MB。我们只需要将 KB 除以 1,000 即可。打印报告的剩余部分，然后进行测试查看使用的交换空间是否超过了 `PC_LIMIT` 变量指定的阈值限制。如果超过了使用百分比，将开启反色显示，显示警告消息并重新关闭反色。列表 18-15 展示了 `SUN_swap_mon.ksh` 脚本的运行情况

```bash
./SUN_swap_mon.ksh
Swap Space Report for wilma
Mon Jun 10 03:50:29 EDT 2007
Total Amount of Swap Space: 590MB
Total KB of Swap Space Used: 66MB
Total KB of Swap Space Free: 524MB
Percent of Swap Space Used: 11.22%
Percent of Swap Space Free: 88.78%
```

列表 18-15 `SUN_swap_mon.ksh` 脚本运行时

注意百分比是以浮点数形式给出的，但有两个额外的零。这两个零是在 `bc` 文档中指定 `scale=4` 然后将结果乘以 100 的。作为一个练习，添加一个命令来移除这两个零。我们结束了吗？还没有；我们还需要一个可以在所有操作系统运行的单一脚本。进入 `all-in-one` 部分。

# 一一体分页与交换空间监控

让我们通过将之前的脚本转为函数并将它们整合，使用 `uname` 命令来确定 UNIX 类型，从而决定运行哪个函数。让我们看看这个合并后的脚本，最后我们将讨论细节。合并后的脚本名为 `all-in_one_swapmon.ksh`，位于列表 18-16 中。

```bash
#!/usr/bin/ksh
#
# SCRIPT: all-in-one_swapmon.ksh
## AUTHOR: Randy Michael
# DATE: 5/31/2007
# REV: 3.0
# PLATFORM: AIX, Solaris, HP-UX and Linux
# PURPOSE: 此脚本用于生成系统分页或交换空间的报告，包括：
#   总分页空间的 MB，空闲分页空间的 MB，
#   已用空间的 MB，使用空间的百分比以及
#   空闲空间的百分比
# REV: 1/5/2007 -- Randy Michael
# REVISION: 添加了 OpenBSD 交换监控函数，
# 根据操作系统修改了 case 语句。
############################
# set -x # 取消注释以调试此脚本
# set -n # 取消注释以检查语法
############################
############# 定义变量 #################
PC_LIMIT=65
# 交换空间百分比上限
# 在发送通知之前
```

列表 18-16 `all-in-one_swapmon.ksh`

# 第 18 章 监控分页与交换空间 631

```bash
THISHOST=$(hostname) # 本地主机名
############################
########### 初始化报告 #################
echo "\nSpace Report for $THISHOST
date
############################
############# 定义函数 #################
function SUN_swap_mon {
    ########### 获取并处理数据 #
# 使用 awk 从 swap -s 输出中提取 $9 和 $11
SW_USED=$(swap -s | awk '{print $9}' | cut -dk -f1)
SW_FREE=$(swap -s | awk '{print $11}' | cut -dk -f1)
# 将 SW_USED 加到 SW_FREE 以获取总交换空间
((SW_TOTAL = SW_USED + SW_FREE))
# 使用替换的 bc 工具计算使用百分比和空闲百分比
PERCENT_USED=$(bc <<EOF)
scale=4
($SW_USED / $SW_TOTAL) * 100
EOF
PERCENT_FREE=$(bc <<EOF)
scale=4
($SW_FREE / $SW_TOTAL) * 100
EOF
# 将 KB 转换为 MB
((SW_TOTAL_MB = SW_TOTAL / 1000))
((SW_USED_MB = SW_USED / 1000))
((SW_FREE_MB = SW_FREE / 1000))
# 输出报告的剩余部分
```

列表 18-16（续）

# 第三部分 系统管理员脚本 632

```bash
echo "\nTotal Amount of Swap Space:\t${SW_TOTAL_MB}MB"
echo "Total KB of Space Used:\t${SW_USED_MB}MB"
echo "Total KB of Space Free:\t${SW_FREE_MB}MB"
echo "\nPercent of Space Used:\t${PERCENT_USED}%"
echo "\Percent of Space Free:\t${PERCENT_FREE}%"
# 获取使用百分比的整数部分
INT_PERCENT_USED=$(echo $PERCENT_USED | cut -d. -f1)
# 检查是否超过了使用百分比的最大阈值
if (( PC_LIMIT <= INT_PERCENT_USED ))
then
# 百比已超过阈值，发送通知
tput rsmso # 开启反色显示！
echo "\nWARNING: Swap Space has Exceeded the ${PC_LIMIT}%\n
Upper Limit!\n"
tput rsmso # 关闭反色显示！
fi
echo "\n"
#####################################
function Linux_swap_mon
{
    ########## 获取并处理数据 ##########
free -m | grep -i swap | while read SW_TOTAL SW_USED SW_FREE
do
    # 使用 here document 中的 bc 工具来计算
    # 空闲和使用交换空间的百分比。
PERCENT_USED=$(bc <<EOP)
scale=4
($SW_USED / $SW_TOTAL) * 100
EOF
PERCENT_FREE=$(bc <<EOP)
scale=4
($SW_FREE / $SW_TOTAL) * 100
EOF
```

列表 18-16（续）

# 第 18 章 监控分页与交换空间 633

```bash
# 生成分页空间的剩余报告：
echo "\nTotal Amount of Swap Space:\t${SW_TOTAL_MB}"
echo "Total KB of Space Used:\t${SW_USED_MB}MB"
echo "Total KB of Space Free:\t${SW_FREE_MB}MB"
```
