
Basic Syntax: `ufsrestore i | r | R | t | x [abcdfhlmostvyLT] ['archive_file'] ['factor'] ['dumpfile'] ['n'] ['label'] ['time-out'] ['filename']...`

where `filename` specifies the pathname of files (or directories) to be restored to disk.

`Ufsrestore` is an incremental file system restore facility used in conjunction with the `ufsdump` facility.

## 23.6.3.6 Script Files for Backup and Recovery

As shown in Chapter 16, user-written script files can be deployed by the system administrator to quickly and efficiently do backup and archiving. Whether they are coded in Python as shown in Chapter 16, or in a shell programming language that embeds any of the preceding command line facilities, they can be used to facilitate and automate the backup, recovery, and archiving of files, directories, or file systems. Additionally, there are several online sources for backup and archiving script files available, and we will not justify the need for planning, coding, or maintaining such script files versus using an online, ready-made program.

The following are two examples of script files, the first one a legacy application of `tar`, and the next one a modern UNIX program for doing backup and archiving. One is coded as Bourne shell scripts, and one is coded as a Python script. They work equally well on PC-BSD or Solaris, with the minor differences in coding for those two systems duly noted in the code.

### Example 23.6: Simple Bourne Shell Example for Automating Tar Backups

The following Bourne shell script will backup `/home/bob` to a directory previously created named `simple_backup` in a compressed format. Use an editor of your choice to create it, and name the script file `backup.sh`:

```
#!/bin/sh

# To backup additional directories, put more pathnames in the following command,

# separated by spaces, such as /home/bob /home/sarwar /home/blahblah.

backup_source="/home/bob"

backup_destination="/home/bob/simple_backup"

filename="back1.tgz"

echo "Backing up your UNIX home directory"

tar cvpzf $backup_destination/$filename $backup_source

echo "Backup Complete"
```

# 练习 23.16

给出使用 `cron` 自动执行前述脚本文件的必要命令，以便每周在凌晨 3:00 运行 `backup.sh` 脚本。可随意修改时间、日期以及源目录和目标目录和文件，以便你可以使用脚本文件在你的 UNIX 系统上备份对你重要的信息。

## 示例 23.7：扩展 Python 脚本示例
使用 `rsync` 进行“滚动”备份

此示例与第 16 章示例 16.30 类似，其显著区别在于它更为详尽，并通过 `ssh` 跨网络复制更多硬链接文件和目录。

基本上，Python 脚本文件执行五个操作：

- 1. 检查是否存在多个编号目录。如果不存在，则创建它们。
- 2. 删除最后一个或最旧的目录。
- 3. 将目录 1 硬拷贝到目录 2。硬拷贝会制作一份共享相同磁盘空间的拷贝（即，你的文件不会占用额外空间）。
- 4. 使用 `rsync` 将你想要的文件备份到目录 1。`rsync` 仅覆盖已更改的文件。此示例遍历本地目录，然后是网络文件。
- 5. 备份源代码。

你应该在 `/home/me/.rsync/exclude` 中创建一个文件，其中包含 `rsync` 要忽略的模式（请参阅 `rsync` 手册了解更多信息）。我们主要排除类似 `*.tmp` 或 `*.o` 的模式。此外，你应该设置 `ssh`，以便可以无需输入密码登录到你的服务器。否则它将无法作为 `cron` 任务工作。

```
#!/usr/bin/python

#
import time
import datetime
import os
import shutil
import UserString

def backupserver():
    debug_flag = "debug"
    sources = ["/etc/aliases", "/etc/resolv.conf", "/etc/hosts",
              "/etc/named.conf", "/etc/group","/etc/dovecot.conf",
              "/var/www/cgi-bin", "/etc/httpd", "/var/www/html"]
    localsources = ["/Volumes/NO NAME/onix", "/Volumes/NO NAME/
                    projects", "/Users/me/myprojects",
                    "/Users/me/bin"]
```

```
localcode = ["/Volumes/NO NAME/projects"]
codetarget = "/Volumes/PC Backups/Code Backups/"
target = "/Volumes/PC Backups/Daily Backups/"
host = "www.mysite.com"
user = "me"
# target can be reached, trigger a rotation of the snapshot
# directories
if (debug_flag == "debug"):
    print "Date: " + str(datetime.date.today())
    print host +" is up, rotating snapshots."
# check to see if directories exist
i = 1
while i <= 5:
    temp_path = target + str(i) + "/"
    if not os.path.exists( temp_path ):
        try:
            os.makedirs( temp_path )
            print "Created " + temp_path
        except:
            print "Couldn't create " + temp_path
    i = i + 1
# cycle backups
# first delete #5
print "Deleting oldest archive"
```
