
- 2. 编辑新创建的脚本文件，以符合 servera 和 serverb 的以下要求。系统使用 SSH 密钥进行身份验证，因此不需要密码。

| 命令或文件 | 请求的内容 |
|---|---|
| `hostname -f` | 获取所有输出。 |
| `echo "######"` | 获取所有输出。 |
| `lscpu` | 仅获取以字符串 CPU 开头的行。 |
| `echo "######"` | 获取所有输出。 |
| `/etc/selinux/config` | 忽略空行。忽略以 `#` 开头的行。 |
| `echo "######"` | 获取所有输出。 |
| `/var/log/secure` | 获取所有 "Failed password" 条目。 |
| `echo "######"` | 获取所有输出。 |

将所需信息保存到工作站 `/home/student` 目录下的 `output-servera` 和 `output-server` 文件中。

> 注意
> 你可以在 servera 主机上无需密码使用 `sudo` 命令。记住使用循环来简化你的脚本。你也可以使用通过管道符 (`|`) 串联的 `grep` 命令。

- 2.1. 使用 `vim` 命令打开并编辑 `/home/student/bin/bash-lab` 脚本文件。

```
$student@workstation ~$ vim ~/bin/bash-lab
```

- 2.2. 将以下行加到 `/home/student/bin/bash-lab` 脚本文件中。

> 注意
> 以下是 Bash 脚本实现所需结果示例。

```bash
#!/bin/bash

OUT='servera serverb'

for server in $OUT; do

    ssh $server "hostname -f" >> /home/student/output-$server

    ssh $server "echo '######'" >> /home/student/output-$server

    ssh $server "lscpu | grep CPU" >> /home/student/output-$server

    ssh $server "echo '######'" >> /home/student/output-$server

    ssh $server "grep -v '^#' -grep -v '^$' /etc/selinux/config" >> /home/student/output-$server

    ssh $server "echo '######'" >> /home/student/output-$server

    ssh $server "grep 'Failed password' /var/log/secure" >> /home/student/output-$server

    ssh $server "echo '######'" >> /home/student/output-$server

done
```

## 总结

- 创建并执行简单的 Bash 脚本以完成简单的管理任务。
- 使用循环在命令行和 shell 脚本中对项目列表进行迭代。
- 使用条件结构在 shell 脚本中引入决策机制。
- 使用正则表达式和 `grep` 命令在日志和配置文件中搜索文本。

# 第 2 章

## 调度未来任务

### 目标

安排任务在特定的日期和时间执行。

### 学习

- 设置一个命令在未来的某个时间运行一次。
- 使用用户的 `crontab` 文件调度命令按周期性计划运行。
- 使用系统 `crontab` 文件和目录调度命令按周期性计划运行。
- 启用和禁用系统定时器，并配置一个管理临时文件的定时器。

### 节目录

- 调度延迟的用户任务（以及指导性练习）
- 调度循环的用户任务（以及指导性练习）
- 调度循环系统任务（以及指导性练习）
- 管理临时文件（以及指导性练习）
- 调度未来任务（测验）

![](img/2eff90170b8c94cce3a908ab927e38c2_52_0.png)

## 调度延迟的用户任务

### 目标

设置一个命令在未来的某个时间运行一次。

### 描述延迟用户任务

有时，你可能需要在特定的未来时间运行一个或多个命令。例如，用户调度了一项在深夜执行的长时间维护任务。另一个例子是系统管理员正在配置防火墙，并队列了一个安全作业，在十分钟后将防火墙重置为工作状态，除非他们在作业运行前禁用了作业且新的防火墙配置已生效。

这些调度命令被称为 *tasks*（任务）或 *jobs*（作业），*deferred* 一表示这些任务将在未来运行。

Red Hat Enterprise Linux 用户调度延迟任务的一种解决方案是 `at` 命令，它是默认安装并启用的。`at` 软件包提供了 at 守护进程，以及与该进程交互的 `at` 和 `atq` 命令。

任何可以查询 `at` 守护进程的用户都可以使用 `at` 命令 `at` 守护进程提供 26 个队列，从 a 到 z 标识，字母顺序靠后的队列具有较低的系统优先级（使用更高的值，详见后续章节）。

### 调度延迟用户任务

使用 `at TIMESPEC` 命令启动一个新的需要调度的作业。`at` 命令从 `STDIN`（你的键盘）读取以获取执行的命令。在手动输入命令时，在行尾按 `Ctrl+d` 完成输入。你可以使用来自脚本的输入重定向来输入更复杂的命令。例如，使用 `at +5min < script` 命令调度 *script* 中的命令在 5 分钟后开始，而无需在终端中手动输入该命令。

`at` 命令接受自然时间规范来描述作业应在何时运行。例如，指定时间为 `22:00pm, 15:59, midnight（午夜）或 tomorrow（明天）`，后面跟着可选的日期或未来数。

`TIMESPEC` 参数期望格式如下的日期时间规范：如果你提供了日期而未提供时间，时间将默认为当前时间。如果你提供了时间而未提供日期，将匹配今天的日期，并在时间匹配时运行作业。

以下示例显示了未提供日期的作业调度。`at` 命令根据时间是否已过，将作业调度在今天或明天。

```
[user@host ~$] date

Wed May 18 21:01:18 CDT 2022

[user@host ~$] at 21:03 < script

job 3 at Wed May 18 21:03:00 2022

[user@host ~$] at 21:00 < script

job 4 at Thu May 19 19:00:00 2022
```

![](img/2eff90170b8c94cce3a908ab927e38c2_53_0.png)

## 第 2 章 | 调度未来任务

`at` 命令的页面和其他文档源在编写自然时间规范时使用小写，但你可以使用小写、句首大写或全大写。以下是你可以使用的时间规范示例。

- `now +5min`
- `teatime tomorrow` (下午 16:00)
- `noon +4 days`
- `5pm august 3 2021`

有关其他有效的时间规范，请参考参考文献列出的 timespec 文档。

### 检查和管理延迟用户任务

要查看当前用户的待处理作业，请使用 `at -l` 命令。

```
[userHost ~5] at

28 Mon May 16 05:13:00 2022 user

29 Tue May 16 17:16:00 2022 h user

30 Wed May 18 12:00:00 2022 user
```
