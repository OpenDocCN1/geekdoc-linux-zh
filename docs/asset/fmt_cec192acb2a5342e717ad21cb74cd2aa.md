
# 让进程休眠

`sleep` 命令暂停进程执行指定的秒数。使用 `sleep` 命令可以在一段时间后导致某个命令执行，或者每隔一段时间执行一次命令。

`sleep` 命令的格式为：

```
$ sleep seconds
```

假设你在工作日期间每小时需要吃药。你可以创建一个 `medicine.ksh` 文件并包含以下内容：

```
print "It is time to take your medicine!"
sleep 3600; print "It is time to take your medicine!"
sleep 3600; print "It is time to take your medicine!"
sleep 3600; print "It is time to take your medicine!"
sleep 3600; print "It is time to take your medicine! Only one more to go!"
sleep 3600; print "It is time to take your medicine! Last time today!"
```

该 shell 脚本可以在后台执行：

```
$ medicine.ksh &
```

# 让进程等待

后台处理是在不需要用户交互时执行长耗时作业的方便方法。然而，你可能需要等待后台作业完成后才能完成其他任务。`wait` 工具会一直等待直到调用者已知的所有进程 ID 终止。

`wait` 命令的格式为：

```
wait [job_name]
```

假设你使用 `ls` 命令配合 `-R` 标志来列出从根目录开始的每个子目录中的所有文件。

假设你需要在编写的脚本中使用这些目录列表。使用 `wait` 命令等待后台作业完成。

此示例演示了在交互式情况下使用 `wait` 命令。

## 示例 10-12: 等待后台作业完成

```
$ ls -lar /usr | grep d > dir-list &
$ wait 586; print "The directory list is complete"
The directory list is complete
$
```

`wait` 是 Korn Shell 的内置命令。由于所有后台作业都是 shell 的子进程，登录 shell 必须等待子进程。

`wait` 命令的选项如表所示。

## 表 10-5：Korn Shell wait 命令选项

| 选项 | 命令 | 等待： |
| --- | --- | --- |
| (无选项) | wait | 所有后台命令完成 |
| %job_number | wait %2 | 作业号 2 完成 |
| process_number | wait 346 | 进程 346 完成 |
| % | wait % | 上一个后台进程完成 |

# 退出状态变量

shell 命令、shell 脚本和系统命令要么：

- 成功并在屏幕上显示结果，或
- 失败并 shell 打印某种诊断性错误消息

shell 还会设置一个预留变量 `?`，存储命令的退出状态。通常设置为：

- 零 (0) 表示执行成功
- 非零表示失败

用户文档描述了特定状态码的含义。在某些情况下，状态码为 1 表示通用的执行错误。

## 示例 10-13: 检查状态

```
$ ls /nonexistent
ls: /nonexistent: No such file or directory
$ echo $?
1
```

# 现在来试试！

1. 输入命令 `ps -al` 以获取所有进程的详细列表。NI 列显示等效 nice 值。
2. 修改命令将其 nice 值设置为 10。

## 解决方案

1. NI 列显示进程优先级。

```
$ ps -al
| F S UID PID PPID %CU PRI NI RSS WCHAN TT TIME COM |
| 8008005 I + 0 348 1 0.0 44 0 56K tty co 0:00:05 get |
| 8008005 S 1731 4423 4422 0.0 41 0 408K wait pl 0:01:01 k |
| 8008005 R N+ 0 4566 4423 0.0 54 10 352K - pl 0:00:04 ps |
```

2. 进程优先级改变了 10。

```
$ nice -n 10 ps -al
| F S UID PID PPID %CU PRI NI RSS WCHAN TT TIME COM |
| 8008005 I + 0 348 1 0.0 44 0 56K ttyin co 0:00:05 get |
| 8008005 S 1731 4423 4422 0.0 41 0 408K wait pl 0:01:01 k |
| 8008005 R N+ 0 4566 4423 0.0 54 10 352K - pl 0:00:04 ps |
```

# 在适当的时间调度作业

```
for_dir.ksh
.
Mon Sat 3 09:44:44 EST 1998
************************************
Cron: 上述消息是其中一个 cron 命令的
标准输出和标准错误。
```

### 现在来一试！

修改在上一个活动中创建的脚本文件，将输出重定向到文件中，然后提交作业在几分钟后运行。

## 解决方案

```
$ cat listing.ksh
date > daily-log.txt
ls >> daily-log.txt
$ at now + 2 minutes listing.ksh
job you.75610265.a at Sat Jan 03 10:17:45 1998
$ cat daily-log.txt
Mon Sat 3 10:17:46 EST 1998
TUTORIAL
daily-log.txt
for_dir.ksh
.
```

# 调度周期性作业

cron 守护进程按照指定的日期和时间定期运行命令。cron 守护进程：

- 在操作系统初始化时启动，并持续运行直到系统故障或关闭
- 创建活动日志
- 定期检查 crontab 以及 `/usr/spool/cron/crontabs` 目录下的文件以查找作业
- 通过以下方式启动 `/usr/spool/cron/crontabs` 目录中的作业：
    - 调用调用进程的 HOME 目录的子 shell
    - 不运行 `.profile` 文件
    - 为每个 shell 提供默认环境，定义 `HOME`、`LOGNAME`、`SHELL(/usr/bin/sh)` 和 `PATH (/usr/bin)`
    - 使用由调用进程存储的作业属性启动作业

# 使用命令

使用 `crontab` 命令将作业放入队列以供 cron 守护进程处理。crontab 命令的输入是一个包含包含命令信息以及你想要执行这些命令的时间的文件。

`crontab [file]` 的格式如下：

```
crontab [file]
crontab -l | -v
crontab -r
```

# 命令选项

crontab 命令选项如表所示。

## 表 10-7：一些 crontab 命令选项

| 选项 | 功能 |
|---|---|
| l | 显示你的 crontab 文件的内容 |
| e | 编辑 crontab 副本；调用由 `EDITOR` 环境变量指定的编辑器，或默认使用 vi。 |
| r | 从 crontab 目录中删除 crontab 文件 |
| v | 详细模式：显示你的 crontab 文件名以及你使用 crontab 提交它的日期和时间 |

以下是一些 crontab 命令示例。

## 示例 10-17：使用 crontab 命令

```
$ crontab -l
$ crontab * * 1 1-5 echo "I was cronned"
$ crontab -v
crontab file: your submission time: Fri Jan 02 13:00:29 1998
```

# 创建 crontab 文件

每个用户同时可以有一个活动的 crontab 文件。crontab 文件可以包含多个条目。文件中的每行由空格或制表符分隔的六个字段组成。

此示例显示了 crontab 文件的格式。

## 示例 10-18：crontab 文件条目

```
0 20 * * 1-5 /usr/adm/cleanup
|   |   |   |   |   
|   |   |   |   | |-----------------------
|   |   |   |   | | 要执行的命令
|   |   |   | | 星期 (0 - 6，0 = 周日)
|   |   |   | |
|   |   | | 日期 (1-31)
```

# 在适当的时间调度作业运行

```
小时 (0-23) 
分钟 (0-59)
```

该示例指示 cron 在每月周一至周五的晚上 8:00 运行程序 `/usr/adm/cleanup`。前五个字段中的每一个都可能包含：

- 数字 数字（在上述所示的范围内）
- 两个由连字符分隔的数字，表示闭区间范围
- 用逗号分隔的列表列表，选择列表中的所有数字
- 星号，表示所有合法值

此示例显示了一个示例 crontab 文件。

## 示例 10-19：典型的 crontab 文件

```
# (@) crontab
#
#
0 5 1 * * /usr/adm/billing
0 20 * * 1-5 /usr/adm/cleanup
```

### 现在来一试！

使用 crontab 调度一个作业进行执行。

a. 创建一个 crontab 文件，将 date 命令的输出捕获到文件 crontab.txt 中。让命令在下一小时内执行三次。
b. 使用 crontab 命令提交文件。
c. 检查作业是否正确执行，然后删除你的 crontab 文件。

## 解决方案

```
$ date
Sat Jan 3 10:36:47 EST 1998
$ cat micron
40,45,50 10 * * date >> crontab.txt
$ crontab micron
$ crontab -l
```

# 总结

## 描述过程

进程是一个程序。

## 获取作业状态

使用 `ps` 命令检查作业状态。

## 控制和管理作业

- 使用 `wait` 命令等待作业完成。
- 使用 `kill` 命令停止作业。在后台运行的。
- 使用 `nice` 命令更改作业的优先级。
- 使用 `sleep` 命令停止。
- 使用 `wait` 命令等待作业完成。

## 在适当的时间调度作业

使用 `at` 命令调度作业运行。

# 11-4 与其他用户通信

## 概述

## 引言

与其他用户电子通信

本单元讨论了如何电子化发送消息。

## 目标

要与其他用户电子通信，你应该能够：

- 发送并接收消息
- 管理邮件

## 资源

有关更多信息，请参阅：
- 常见主题：电子邮件

# 使用 Mailer (CDE)

## 概述

CDE 提供了用于与其他用户通信的 Mailer。使用 Mailer，你可以：

- 发送并接收消息
- 管理你的邮件

## 启动

要启动 Mailer，点击界面上的 Mailer 控制。

点击控制后，Mailer 将显示主窗口。

## 图 11-1：Mailer 的主窗口

## 主窗口

Mailer 的主窗口由以下组件组成：

| 组件 | 功能 |
|---|---|
| 消息头部列表 | 显示消息 |
| 消息视图区域 | 显示正文 |
| 标题 | 允许创建带附件的消息 |
| 附件窗口 | 包含附件的图标 |

# 使用 Mailer CDE

## 示例 11-1：Mailer 的主窗口

```
/spool/mail/joe
Mailbox Edit View Compose Help
Sender Subject Date
cindy@users let's go to see... May
cindy@users Re: Meeting on Thursday
mike@users RE: Meeting on Thursday
今晚去看 泰坦尼克号
```

# 创建邮件消息

要创建邮件消息，从 Compose 菜单中选择新消息。Mailer 显示的新消息所示。

## 示例 11-2：新消息

```
New Message
File Edit Attachments Format
To: mike@users
Subject: Re: Meeting on Thursday
Cc: joe
Hi,
Cindy 将参加我的会议。我将去度假。
0 附件
Send Close
```
