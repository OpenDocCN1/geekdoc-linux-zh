
在备份作业成功提交给目录后，你可以使用 `status` 命令跟踪其状态。你也可以使用 `messages` 命令在更新到达时获取逐条更新。取决于你对系统 Message 资源的设置，一份详细的总结报告可能会通过电子邮件发送给 Bacula 管理员。

## 执行恢复作业

要恢复文件，请启动控制台并运行 `restore` 命令。`run` 命令中的 `restore` 是菜单驱动的。它首先帮助你识别哪些作业需要恢复到目标文件。通过 `restore` 方法可以指定相关的 Job ID。一旦你选择了一组作业，就可以从这些作业中选择要恢复的文件。

- `restore`
  要选择 JobIds，你有以下几种选择：
  1: 列出最后运行的 20 个作业
  2: 列出保存了指定文件的作业
  3: 输入用逗号分隔的 JobIds 列表进行选择
  4: 输入 SQL 列表命令

运行恢复作业

- 选择客户端最近的备份
- 选择指定时间之前的客户端备份
- 输入要恢复的文件列表
- 输入指定时间之前的要恢复的文件列表
- 查找该客户端最近备份的 Jobids
- 查找该客户端指定时间之前的备份的 Jobids
- 为找到的 Jobids 输入要恢复的目录列表
- 取消

Select item: (1-12):

三个最有用的选项是“选择客户端最近的备份” (#5)、“选择指定时间之前的客户端备份” (#6) 以及“列出保存了指定文件的作业” (#2)。前两个选项提供了一个类似 shell 的选择环境，类似于 `restore -i`。此选项对于那些永远记不住自己删除的文件具体在何处的烦人用户来说非常方便。另一个查找 Job ID 的强大方法是选项 #4，“输入 SQL 列表命令”，它允许你输入任何格式正确的 SQL 查询语句。（当然，你必须熟悉数据库模式。）

假设一个用户需要恢复一份他们的 `pw_expire.pl` 脚本。然而，他不确定文件在哪个目录中。此外，他还希望将文件恢复到原始机器的 `/tmp` 目录。这样的请求会让系统管理员在饮水机旁抱怨个不停，但对于 Bacula 管理员来说这轻而易举。（不幸的是，Bacula 的搜索范围非常广，我们必须在下面进行截断。）

- `restore`

- 要选择 JobIds，你有以下几种选择：
  - 列出最后运行的 20 个作业
  - 列出保存了指定文件的作业

Select item: (1-12): 2
Defined Clients:

- `bull`
- `harp`

| Job | Name | StartTime | JobType... |
| :--- | :--- | :--- | :--- |
| 4484 | /home/jim/development/pw_expire.pl | 2009-01-23 20:11:35 | B... |
| 4251 | /home/jim/development/pw_expire.pl | 2009-10-21 18:03:01 | B... |
| 4006 | /home/jim/development/pw_expire.pl | 2009-10-06 20:10:02 | B... |

Bacula 的 `pw_expire.pl` 实例列表显示了几个最近的备份及其相关的 Job ID。Bacula 然后将我们带回恢复菜单，我们可以使用选项 #3（输入作业 ID）来关注特定的作业。

Select item: (1-12): **3**
Enterid(s), comma separated, to restore: **4484**
You have selected the following Jobid 4484
Building tree for Jobid 4484 ... 1 Job, 779,470 files
You are now进入文件选择模式，可以在此模式下添加（标记）和移除（取消标记）要恢复的文件。文件最初会被添加，除非

输入 "done" 退出此模式。

```
cwd is /
```

```
$ /home/jim/development
```

```
cwd is:/home/jim/development
```

```
$ dir
```

```
-rwx-xr-x 1 jim atrium 923 2009-10-25 12:05:43 /home/jim/development/pw_exp...
```

```
$ mark pw_expire.pl
```

```
1 files marked
```

```
$ done
```

此示例中未显示，但 Bacula 有时会显示带逗号的作业 ID（例如 4484）。在向 Bacula 输入任何 ID 时，必须省略逗号；否则 Bacula 会将你的输入解释为逗号分隔的列表。写入 `/var/bacula/working/restore.bsr` 的引导记录
作业将需要以下卷：

```
1 file selected to be restored.
```

Defined Clients:

- 1: bull
- 2: harp

Select the Client (1-2): **2**

Bacula 现在写入它将用于执行恢复的引导文件，显示它所需的磁带卷，并提示你选择一个客户端，以便将其文件恢复回原始主机。

```
Run Restore Job

JobName: RestoreFiles

Bootstrap: /bacula/working/restore.bsr

Where: /var/restore

Replace: always

FileSet: Full

Backup Client: harp

Restore Client: harp

Storage: LTO-4000

When: 2009-11-23 15:13:55

OK: 10

OK to run? (yes/no):
```

在运行此作业之前，我们需要修改设置。

OK to run? (yes/no): mod

Parameters to modify:

1: Level

2: Storage

3: Job

4: FileSet

5: Client

6: When

7: Priority

8: Bootstrap

9: Where

10: Replace

11: Job

Select item to modify (1-12): 9

Please enter path for restore (for none): /tmp

```
JobName: RestoreFiles
Bootstrap: /bacula/working/restore.bsr
Where: /tmp
```

OK to run? (yes/no): yes

Run command submitted.

Restore done

## 备份 Windows 客户端

你可以从 bacula.org 下载 Windows 客户端的二进制文件。

Bacula 备份 Windows 数据非常出色，但需要额外的步骤来处理状态。为了正确捕获锁定的文件，你可能需要使用 Windows 影拷贝服务 (VSS)。检查 Bacula 示例目录获取其他 Windows 技巧，包括一个触发系统状态的脚本。最新版本的 Bacula 支持 Windows 7 和 64 位。甚至支持 Exchange 备份。

## 监控 Bacula 配置

系统管理需要警惕，备份是最后一道防线。如果不及时修复，关键数据将会丢失。

Bacula 作业会根据目录配置中的 Message 资源生成作业报告。报告包含了使用的卷、备份的文件数量和大小，以及可能发生的错误。我们建议将消息发送到你的收件箱，或者传呼机。

你可以使用控制台的 `status` 命令查询各种 Bacula 守护进程。输出包含了即将进行的作业、正在运行的作业以及已终止的作业。`messages` 命令是查看日志条简单方法。

Bacula 包含一个 Nagios 插件，可以轻松集成到现有的监控基础设施中。有关 Nagios 的一般信息见。

## Bacula 技巧

常见问题包括客户端进程未运行以及存储守护进程找不到追加卷。在下面的示例中，目录进程报告备份作业因无法与文件进程通信而终止。此错误会在报告末尾重复。

- SD termination status: Waiting on FD

*** Backup Error ***

- 11-Nov 21:06 bull-dir Jobid 259: Warning: bock:c.123 Could not connect to Client on 192.168.1.9102. ERR=Connection refused Retrying ...

- 11-Nov 21:31 bull-dir Jobid 259: Warning: bock:c.123 Could not connect to Client on 192.168.1.9102. ERR=Connection refused

示例显示存储守护进程报告没有相应的池卷可执行请求的备份。你可以通过向池中添加新卷或清理并回收现有卷来修复此错误。不需要重启进程；Bacula 应该一直执行直到式调用。
