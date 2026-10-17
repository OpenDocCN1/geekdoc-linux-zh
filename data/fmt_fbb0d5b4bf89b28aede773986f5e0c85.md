
```
0 9 * 1-5 mutt -s "Checking in" boss@example.com % Hi there, just checking in.
```

参考文献

`crond(8)`, `crontab(1)` 以及 `crontab(5)` 手页

## 引导练习

### 调度周期性任务

在此练习中，你将使用 `crontab` 命令以非权限用户身份按周期调度命令。

## 预期结果

你应该能够：

- 以非权限用户身份调度周期任务。
- 检查周期任务执行的命令。
- 删除周期任务。

## 准备工作

使用 `student` 作为密码登录 `workstation`。

在 `workstation` 上运行 `lab scheduling-cron start` 开始练习。该脚本确保环境整洁且配置正确。

```
[student@workstation ~]$ lab scheduling-cron start
```

1. 从 `workstation` 以 `student` 身份 SSH 连接到 `servera`。

```
[student@workstation ~]$ ssh student@servera
...省略...
[student@servera ~]
```

2. 以 `student` 调度一个周期任务，每天上午 8 点到晚上 9 点之间每两分钟将当前日期和时间更新到 `/home/my_first_cron_job.txt`。该任务必须在周一至周五运行，周六或周日不运行。

> 重要
> 如果你在上述指令提到的时间段之外进行实验，应相应地调整你的系统时间和或日期，以便任务在你工作期间运行

2.1. 使用 `crontab -e` 命令使用默认文本编辑器打开 `crontab`。

```
[student@servera ~]$ crontab -e
```

2.2. 插入以下行。

## 第 2 章 调度未来任务

```
*208-20 * * Mon-Fri /usr/bin/date >> /home/student/
my_first_cron_job.txt
```

2.3. 在编辑器中，按 `Esc` 键并输入 `:wq` 保存更改并退出编辑器。当编辑退出时，看到以下输出：

```
...省略输出...
crontab: installing new crontab
[student@servera ~]$
```

上述输出确认了 `crontab` 已成功调度。

3. 使用 `crontab -l` 列出已调度的周期性作业。检查你在上一步中调度的作为周期性作业运行的命令。

```
[student@servera ~]$ crontab -l
*/08-20 * * * * >> /home/student/my_first_cron_job.txt
```

注意，调度的任务会运行 `/usr/bin/date` 命令，并将其输出追加到 `/home/student/my_first_cron_job.txt`。

4. 使用 `while` 命令，使你的 shell 提示符休眠，直到由于周期性作业成功执行而了 `/home/student/my_first_cron_job.txt` 文件。等待 shell 提示符返回。

```
[student@servera ~]$ while ! -f my_first_cron_job.txt; do sleep 1;
done
```

上述 `while` 命令使用 `test -f` 继续运行 `sleep 1` 循环，直到 `/home/student` 目录下创建了 `my_first_cron_job.txt` 文件。

5. 使用 `cat` 命令验证 `/home/student/my_first_cron_job.txt` 的内容是否与 `date` 命令的输出匹配。

```
[student@servera ~]$ cat my_first_cron_job.txt
Fri Mar 22 13:56:01 IST 2019
```

上述输出可能根据你的系统有所不同。

## 第 2 章 | 调度任务

6. 删除所有以 `student` 身份运行的周期性作业。

6.1. 使用 `crontab -r` 命令删除 `student` 的所有调度周期性作业。

```
[student@servera ~$] crontab -r
```

6.2. 使用 `crontab -l` 命令验证 `student` 不再存在周期性作业。

```
[student@servera ~] crontab -l
no crontab for student
```

6.3. 退出 `servera`。

```
[student@servera ~]$ exit
logout
Connection to servera closed.
[student@workstation ~]$
```

## 完成

在工作站上，运行 `lab scheduling-cron finish` 来完成此练习。该脚本将删除整个练习过程中创建的文件，并确保环境是洁洁的。

```
[student@workstation ~]$ lab scheduling-cron finish
```

此引导性练习结束。

## 调度周期性系统作业

## 目标

完成本节后，你应该能够使用系统 `crontab` 文件和目录调度按周期性计划运行的命令。

### 描述周期性系统作业

系统管理员经常需要运行周期性作业。最佳实践是从系统账户而非用户账户运行这些作业。也就是说，不要使用 `crontab` 命令调度运行这些作业，而是使用系统范围的 `crontab` 文件。系统范围 `cron` 文件中的作业条目与用户的 `cron` 条目相似，唯一的区别是系统范围 `cron` 文件有一个额外的字段来定义命令字段；即运行该命令的权限用户。

`/etc/crontab` 文件在包含的注释中有一个实用的语法。

```
# 详情请参 man 4 crontabs
# 作业定义示例：
# | 分 (0 - 59)
# | 小时 (0 - 23)
# | 日期 (1 - 31) 或 jan,feb,mar,apr...
# | 月份 (1 - 12) 或 (星期日=0 或 7) sun,mon, tue
# | 星期 (0 - 6)
# * * * * 用户-name 要执行的命令
```

周期性系统作业定义在两个位置：`/etc/crontab` 文件和 `/etc/cron.d/` 目录内。你应该调度周期性系统作业。将自定义 `crontab` 文件放置在 `/etc/cron.d` 中，以防止被 `/etc/crontab` 提供者发生的任何包更新所覆盖，后者可能会覆盖现有条目。需要周期性系统作业的包会将其 `crontab` 文件放在 `/etc/cron.d/` 中。管理员还使用此位置将相关作业分组到一个文件中。

`cron` 系统还包含了需要每小时、每天、每周和每月运行的脚本仓库。这些仓库是目录 `/etc/cron.hourly/`、`/etc/cron.weekly/` 和 `/etc/cron.monthly/`。再次，这些目录包含的是可执行脚本，而不是 `cron` 文件。

> 重要
> 记住将放置在这些目录中的任何脚本设置为可执行。如果脚本不可执行的，它将无法运行。要使脚本变为可执行，请使用 `chmod +x script_name`。

## 第 2 章 | 调度任务

从 `/etc/cron.d/@hourly` 文件调用的名为 `run-parts` 命令运行 `/etc/cron.hourly/*` 脚本。`run-parts` 命令还会运行每日、每周和每月作业，但它是从一个名为 `/etc/anacontab` 的不同配置文件调用的。

> 在过去，使用一个独立的服务 `anron` 来处理 `/etc/anacontab` 文件，但在 Red Hat Enterprise Linux 7 及更高版本中，常规 `cronond` 服务解析此文件。

`/etc/anacontab` 的目的是确保重要作业始终运行，而不会在作业应该执行时因系统关闭或休眠而被意外跳过。例如，如果一个系统作业每天运行，但上一次由于系统正在重启而没有执行，则该作业在系统恢复时执行。然而，取决于系统恢复，启动作业可能有几分钟的延迟。

`/etc/anacontab` 的目的是确保重要作业始终运行，而不会在作业应该执行时因系统关闭或休眠而被意外跳过。例如，如果一个系统作业每天运行，但上一次由于系统正在重启而没有执行，则该作业在系统恢复时执行。然而，取决于系统恢复，启动作业可能有几分钟的延迟。

`/etc/anacontab` 的目的是确保重要作业始终运行，而不会在作业应该执行时因系统关闭或休眠而被意外跳过。例如，如果一个系统作业每天运行，但上一次由于系统正在重启而没有执行，则该作业在系统恢复时执行。然而，取决于系统恢复，启动作业可能有几分钟的延迟。
