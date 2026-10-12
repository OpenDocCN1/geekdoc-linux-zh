
`vim /etc/crontab`

```
SHELL=/bin/sh
PATH=/usr/bin:/usr/sbin:sbin:/usr/lib/news/bin
MAILTO=root
20 * * * root mail student1 < /var/log/messages
```

## 本章总结

这里是系统`cron`表的一个示例：

以下列表描述了该系统`cron`表的每一行：第一条目定义了`cron`表在运行调度任务时使用的`shell`。在`OpenSUSE`中，系统`cron`表使用`Bourne`（由`sh`标示）。

- `SHELL=/bin/sh`
- `PATH=/usr/bin:/usr/sbin:sbin:/usr/lib/news/bin`—此条目定义了`PATH`变量（在第5章中解释）。系统`cron`表使用此条目在`cron`表中搜索命令。如果未定义`PATH`，则必须使用命令的绝对路径，例如：`20 * * * root /bin/student1 < /var/log/messages`
- `MAILTO=root`—此条目定义了`MAILTO`变量。从`cron`表运行的命令的输出将发送给`MAILTO`变量定义的用户。示例`cron`表中的命令没有输出，因此不会向`root`发送电子邮件。
- `20 * * * root mail student1 < /var/log/messages`—这是调度任务，它看起来与`cron`表中的调度任务相似。系统`cron`表的前五个字段与`cron`表的前五个字段相同。唯一的区别在于第六个字段。在系统`cron`表中，第六个字段定义了运行命令的用户。在前面的示例中，它是`root`用户。

![](img/b8a4c65ba2acb99909d8842055c0bdd7_160_0.png)

此系统`cron`表被设定为每20分钟通过电子邮件发送系统日志消息（位于`/var/log`目录中）。

## 本章总结

- 应该定期备份几个目录，特别是用户的主目录。
- `Linux`包含了备份工具，如`tar`和`cpio`，用于将文件备份到归文件中。
- 归文件被解压以恢复数据。

## 关键术语

- `archive` (归档文件)：一个包含许多文件的文件，例如备份。
- `compression` (压缩)：减小数据大小的过程。
- `copy-in`：创建归文件时使用的`cpio`模式。
- `copy-out`：提取时使用的`cpio`模式。
- `copy-pass`：将文件从一个目录复制到另一个目录而不创建归文件时使用的`cpio`模式。
- `cron table` (cron 表)：调度任务的配置。
- `full backup` (全备)：包含所有文件的0级备份。
- `incremental backup` (增量备份)：仅包含上次备份以来更改的文件。
- `members` (成员)：归文件中的文件。
- `snapshot file` (快照文件)：用于识别哪些文件发生了的文件。
- `standard input` (标准输入)：输入源，通常是键盘。
- `standard output` (标准输出)：输出通常是屏幕。

## 复习题

1. 你应该备份以下哪些目录？（选择所有适用项）
   a. `/etc`
   b. `/home`
   c. `/bin`
   d. `/usr/bin`

2. 一名员工想将主目录备份到一个文件中。应该使用以下哪条命令？
   a. `tar -cvf home.tar /home`
   b. `tar -cvf home.tar`
   c. `tar -xvf home.tar /home`
   d. `tar -xvf /home`

3. 你应该使用以下哪条命令列出`project.tar`中的所有成员？
   a. `tar -cvf project.tar`
   b. `tar -lvf project.tar`
   c. `tar -xvf project.tar`
   d. `tar -tvf project.tar`

4. 一名员工抱怨她的主目录消失了。你应该使用以下哪条命令提取备份？
   a. `tar -cvf home.tar`
   b. `tar -xvf home.tar`
   c. `tar -ef /home`
   d. `tar -ef /home`

5. `tar`使用以下哪个选项向归文件中添加成员？
   a. `-u`
   b. `-r`
   c. `-A`
   d. `-d`

6. 解释快照文件的作用。

7. 解释全备和增量备份的区别。

8. 创建归文件时使用的`cpio`模式是：
   a. `copy-in`
   b. `copy-out`
   c. `copy-pass`
   d. `copy-from`

9. 将文件从一个目录复制到另一个而不创建归文件时使用的`cpio`模式是：
   a. `copy-in`
   b. `copy-out`
   c. `copy-pass`
   d. `copy-from`

10. 你的公司预算紧张，被要求创建归文件以节省备份介质空间。以下哪条命令允许你同时归档并压缩主目录？
    a. `tar -czf home.tar.gz /home`
    b. `gzip -v /home`
    c. `bzip2 -v /home`
    d. `tar -cvf home.tar.gz /home`

11. 描述`cron`表的前五个字段。

12. 用户`cron`表和系统`cron`表的区别是什么？

## 案例项目

### 案例项目 6-1：归档主目录

![](img/b8a4c65ba2acb999090bdd7_163_0.png)

你是东海岸职业学院的`Linux`系统管理员。自从`Thompson`博士将学校的计算机基础设施从`Windows`切换到`Linux`后，你一直在教老师如何使用`openSUSE`。现在学期过去了，你意识到许多老师的主目录下都有必须备份的重要文件。写一个管理员可以使用来归档老师主目录的`tar`命令。为归文件添加数字标记为“Backup of home directory.”

- 在`/etc/passwd`和`/etc/shadow`配置文件中识别关键的用户账户信息
- 描述`/etc/login.defs`和`/etc/default/useradd`配置文件中的默认用户和组信息
- 在命令行创建并修改用户账户
- 在命令行创建并修改组
- 使用`YaST`工具管理用户和组账户

## 管理用户

在第6章中，你学习了如何使用命令行工具备份你的`Linux`文件系统。在本章中，你将探索与用户和组的操作。你首先将检查用于身份验证的配置文件以及包含用户账户信息的数据库文件。接下来，你将学习如何在命令行中创建和修改用户及组账户。最后，你将学习如何使用`YaST`工具管理用户和组。

为了让用户登录`Linux`计算机、访问资源并根据其账户权限执行操作，必须通过身份验证确认其账户有效。身份验证是通过与中央用户数据库检查其用户名或密码来验证某人身份的过程。在`Linux`中，用户数据库由两个配置文件组成：`/etc/passwd`和`/etc/shadow`。

`Linux`配置取决于`Linux`发行版而异。与所有配置文件一样，在进行更改之前，你应该创建一个备份。

![](img/b8a4c65ba2acb99909d8842055c0bdd7_165_0.png)

### /etc/passwd 文件

`/etc/passwd`文件包含账户信息。每个条目都有由冒号分隔的字段。每个人都有权限查看此文件的内容（有时被称为“世界可读”文件，因为每个人都可以查看它）。以下列表解释了`/etc/passwd`文件示例中的每个字段：

```
amber:1000:Amber Dawn:/home/amber:/bin/bash
```
