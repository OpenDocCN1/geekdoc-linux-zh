
### 初始化

```bash
timestamp=$(date +%YdT%T%M) # "T" 代表时间；示例：Oct02T095800
Alert_Info=$tmp/\$Alert_info # "$" 是我们脚本唯一的 PID/ID。
server_name=$(hostname -n)
LOG_FILE=/home/logger/ROSETTY/LOGS/check_coredump.sh $timestamp
MMDD=$(date + "%b %d") # 示例：'Oct 02'
ZZZ_error_log=/logger/ROSETTY/ZZZ_error_log.$MMDD
coredump=/home/logger/ROSETTY/temp/
current=示例: 现在是早上 8 点；17 是下午 5 点
day_of_week=$(date +%a) # 示例：'Sun' 代表周日
# 注意：第一行的输出会将 'Oct 02' 更改为 'Oct 2'
# 第一行中的 'sed' 会将 'Oct 02' 更改为 'Oct 2' | sed 2>/dev/null
# 有关前一行的更多信息，请参阅
# 名为 check_coredump.ksh 的脚本中关于 SED 的注释
# 初始化结束。
```

### 函数定义

```bash
############################
function create_testfiles {
  # 函数开始
  # 创建 2 个测试文件：1. ZZZ_error_log 2. coredump
  print "ApplicationZZZ LOG" >$ZZZ_error_log
  print "Error message: BEA-142 UNABLE TO REACH EXTERNAL SERVER." >>$ZZZ_error_log
  # 注：“BEA-142 并不是真实的错误信息；
  # 该错误信息的目的是帮助
  # 我们演示此脚本的功能。

  # 创建一个 1 行的转储文件：
  print "UNABLE TO ESTABLISH DATABASE CONNECTIVITY" >$coredump
} # 函数结束
```

### 主逻辑

#### 脚本开始时的清理工作
`clear` 清空用户会话。

#### 显示联系信息

```bash
# 如果用户在命令行输入 ./check_health.ksh，则显示手机号码：
if [ "$1" = "phone" ]; then
  print "\n注释：这是脚本 .0"
  print "目的：检查 Application.ZZZ 的“健康状况”。"
  print "\n支持团队："
  print "1. Larry Smith, (555) 111-3311, larry@three_stoges.com"
  print "2. Moe Howard, (555) 222-2222, moe@three_stoges.com"
  print "3. Joe Carly, (555) 333-3333, joe@three_stoges.com"
  print "\n热线服务台：1-800-999-9999\n"
fi
```

```bash
# 执行为我们创建两个测试文件的函数：
create_2testfiles
```

#### 日志标题

```bash
# 为此脚本的日志文件中添加标题：
print "CURRENT DATE: $timestamp SERVER: $server_name" >>$LOG
print "Comment：这是脚本 .0" >>$LOG
print "\nCheck on the 'health' of Application.ZZZ." >>$LOG
print "LOCATION of this script's: $LOG"
```

#### Alert-Info 标题

```bash
# 在 Alert-Info 文件中添加标题（如果发现严重问题，
# 将将其发送给所有员工）：
print "\n### START OF ALERT INFO ###" >>$Alert-Info
print "CURRENT DATE: $timestamp SERVER: $server_name" >>$Alert-Info
print "Comment：这是由 .0 创建的 Alert-Info 文件" >>$Alert-Info
print "Alert status: Application.ZZZ problems。" >>$Alert-Info
###### 脚本结束清理工作 #######
```

### 检查 ApplicationZZZ 是否运行

```bash
####################################################################################
# ## 检查 ApplicationZZZ 是否运行：
# 详情请参阅脚本 "bring_up_application.ksh"。

current_hr=$(date +%X) # 示例：早上 8 点，17 是下午 5 点
day_of_week=$(date +%A) # 示例：'Sun' 代表周日

# 如果不是周日，且时间在早上 8 点到下午 5 点之间，
# 那么 applicationZZZ 应该是：
if [[ $day_of_week != "Sun" && $current_hr -gt 7 && $current_hr -lt 18 ]]; then
  ZZZ_should_be_up="Y"
else
  ZZZ_should_be_up="N"
fi

# 检查 applicationZZZ 是否处于状态：
if [ $(ps -ef | grep 'applicationZZZ' | grep -v 'grep') -eq 0 ]; then
  ZZZ_is_up="N"
else
  ZZZ_is_up="Y"
fi

# 如果 applicationZZZ 宕机且未启动，则
if [[ "$ZZZ_should_be_up" == "N" && "$ZZZ_is_up" == "Y" ]]; then
  print "\nNOTHING TO REPORT" >>$LOG
  print "applicationZZZ is down and is not up" >>$LOG
```

#### 字符串信息

`strings` 在核心转储（`coredump`）中找到以下信息：
能够建立数据库连接

#### 今日行信息

来自 `/home/lady/ROSETTA/LOGS/ZZZ_error_log.Apr25` 的最新行如下：
`ApplicationZZZ` 错误日志
`Apr25.T13912` 错误: `BEA-E1142` 无法到达外部服务器。

问题：`densvr27` 无法 `ping` 通。

#### 警报信息结束

时间戳：`Apr25.T13912` 脚本：`./check_health.ksh`

### 程序 `check_health.CRON.sh`

```bash
程序：check_health.CRON.sh
#!/bin/bash
# 程序名：check_health.CRON.sh
# 目的：1. 检查应用程序的“健康状况”。
# 2. 显示如何使用 "crontab" 执行任务。
# 编写者：Larry Smith。由 __ 于 __ __日期__ 修订。
# 难度：中级
# 用法：check_health.CRON.sh (由 crontab 执行)
# 脚本执行后，你想查看的日志位于：
# home/lady/ROSETTA/LOGS/check_health.$1timestamp
# 注意：# UNIX 和 LINUX 操作系统提供了一个免费且非常棒的
# 工具，允许你调度任务，以便系统可以在
# 任何时间（任何日期）执行（运行）该任务。
# 更多详情，请参阅此书中名为 CRON.txt 的文件。
```

此脚本由 `cron` 每隔 15 分钟执行一次，

从周一至周六（1-6）的上午 8 点到下午 5:45 (17:45)：

`00,15,30,45 08-17 * 1-6/home/lady/ROSETTA/LOGS/check_health.CRON`

- 该脚本生成的你应该测试的任何输出行（包括错误！）会被放置在一个日志文件中。
- 在将其添加到 `crontab`（参见 `file.txt`）之前，你应当从命令行执行该任务：`./check_health.CRON.sh`

如果你的屏幕上没有任何输出（什么都没有！），为什么看到类似 "`DONE. Script: ...`" 的内容没什么坏处？

当 `cron` 运行相同的任务时，显示在你的屏幕上的任何输出
