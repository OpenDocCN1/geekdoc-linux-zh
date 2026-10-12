
## 列表 13.3 继续

```
-rw-r--r-- 1 tschenk staff 2230 Mar 9 00:37 page.c
-rw-r--r-- 1 tschenk staff 6371 Mar 9 00:37 parse.c
[tschenk@marcanthony work]$ rm foo *
rm: cannot remove 'foo': No such file or directory
rm: remove '-Makefile'?
```

启用 rm 别名后，用户在文件实际被删除之前会收到提示，从而能够意识到自己的错误，而不必承受数据丢失的后果。你不会被打断，生活很美好。不幸的是，许多用户觉得删除文件的提示很烦人，于是关闭了这些别名。我总是尝试鼓励用户保留这些别名，因为我自己也多次被这种简单技巧拯救过。

## 使用 RCS 跟踪文件

另一种用户可以采用来保护重要文件的方法是使用 RCS 或 CVS 等版本控制系统。版本控制系统允许用户跟踪文件的更改，通常通过存储原始文件然后使用增量来跟踪更改。在列表 13.4 中，你可以看到使用 RCS 如何让用户从管道和重定向示例中发生的 fstab 文件丢失中恢复过来。

### 列表 13.4 使用 RCS 防止数据丢失的简单示例

```
[tschenk@marcanthony foo]$ ls -l
total 4
-rw-r--r-- 1 tschenk staff 912 Mar 14 01:13 fstab
[tschenk@marcanthony foo]$ mkdir RCS
[tschenk@marcanthony foo]$ ci -u fstab
RCS/fstab,v <-- fstab
enter description, terminated with single '.' or end of file:
NOTE: This is NOT the log message!
>> Filesystem table
>> .
initial revision: 1.1
done
[tschenk@marcanthony foo]$ ls -l
total 8
drwxr-xr-x 2 tschenk staff 4096 Mar 14 01:14 RCS
-r--r--r-- 1 tschenk staff 912 Mar 14 01:15 fstab
[tschenk@marcanthony foo]$ co -u fstab
RCS/fstab,v --> fstab
revision 1.1 (unlocked)
done
```

### 列表 13.4 继续

```
[tschenk@marcanthony foo]$ ls -l
total 8
drwxr-xr-x 2 tschenk staff 4096 Mar 14 01:14 RCS
-rw-r--r-- 1 tschenk staff 912 Mar 14 01:15 fstab
[tschenk@marcanthony foo]$ cat fstab | sed 's/ext2/ext3/' > fstab
[tschenk@marcanthony foo]$ ls -l
total 4
drwxr-xr-x 2 tschenk staff 4096 Mar 14 01:14 RCS
-rw-r--r-- 1 tschenk staff 0 Mar 14 01:15 fstab
[tschenk@marcanthony foo]$ co -l fstab
RCS/fstab,v --> fstab
revision 1.1 (locked)
writable fstab exists; remove it? [y/n]: y
done
[tschenk@marcanthony foo]$ ls -l
total 8
drwxr-xr-x 2 tschenk staff 4096 Mar 14 01:18 RCS
-rw-r--r-- 1 tschenk staff 912 Mar 14 01:18 fstab
```

在这个示例中，用户在当前目录下创建了一个名为 RCS 的目录，并使用 ci 命令签入文件的当前版本。为了随后对文件进行操作，用户使用带 -l 选项的 co 命令签出并锁定文件。用户现在像在列表 13.2 中那样运行 sed 命令，结果相同。然而，这次用户只需再次使用 co -l 命令从 RCS 中签出当前修订版，并在提示时回答 yes 即可恢复文件内容。这会将文件恢复到原始状态，我们就可以再次尝试替换，这次使用临时文件来避免错误。这看起来可能工作量很大，但除了能够恢复丢失的文件外，它还有其他优点。通过使用 RCS 或 CVS 保存重要文件，并在签入文件时输入有意义的日志消息，可以使用另一个 RCS 命令 rlog 轻松确定文件的更改情况。使用 RCS 还可以轻松确定是否有人不当更改了文件，因为它提供了 rcsdiff 命令来比较文件与最新签入的修订版。这假设你始终在对文件进行操作时正确签出文件，并在完成后签入更改。

## 创建个人备份

另一种用户可以采用的简单技术是为了防止因我们一直在讨论的此类错误而导致数据丢失而创建个人备份。这些备份可以通过一个简单的 shell 脚本来实现，该脚本从夜间 cron 作业运行，创建要保护的重要文件的 tar 归档。列表 13.5 就是这样一个脚本的示例，它会备份用户主目录中过去 24 小时内更改的任何文件，并将它们存储在用户定义的目录中的文件中。

### 列表 13.5 使用 tar 的简单个人备份脚本

```bash
#!/bin/bash

# First create a basename for the tar file consisting of the username
# and the current date.
TODAY=`date +%Y%m%d`
ARCHNAME="${USER}_${TODAY}"

# Specify a list of directories under my home directory to backup.
BACKUPDIRS="Mail projects docs"
STORAGE=${HOME}/.archives

# Loop through our list of backup directories and for each one, create
# an incremental backup of all files modified within the last two days
# so that each file resides in at least two different backup files.
for DIR in ${BACKUPDIRS}; do
  ARCHNAME="${ARCHNAME}_${DIR}"

  /usr/bin/find $HOME/$DIR -mtime -2 -print \
    | /bin/tar cvzf ${STORAGE}/${ARCHNAME}.tar.gz -T -

done

exit 0
```

用户只需修改 BACKUPDIRS 变量和 STORAGE 变量的定义以满足其需求，然后创建 crontab 条目使其每晚运行一次即可使用此脚本。使用这种方法，用户可以在向系统管理员请求从系统备份中恢复之前，先尝试从个人备份中恢复文件。这对于你的系统来说可能是一个好选择，也可能不是，取决于工作站的磁盘空间或用户可能尝试存储备份文件的共享文件系统的磁盘空间。

## 使用 sudo 限制 root 访问

这些措施可应用于普通用户以及具有 root 访问权限的用户。然而，还可以采取另一项额外措施：使用 sudo 限制对 root 权限的访问。对于用户出于正当理由需要以 root 权限访问系统的那些情况，使用 sudo 授予此访问权限，并将访问权限限制为用户执行其工作所需的命令。给普通用户系统 root 权限通常不是一个好主意。然而，通过使用 sudo，你不仅限制了访问，还获得了用户正在执行的命令的日志记录的好处。当用户尝试执行你未授予其作为 root 执行的操作时，你还会收到警告。有关 sudo 用法的更多信息可在第 27 章“安全管理员工具箱”中找到。

现在我们已经介绍了可能导致数据丢失的常见用户错误，我们可以继续讨论我们作为系统管理员必须处理的下一个数据丢失场景：病毒、特洛伊木马和其他破坏性软件。

## 病毒和其他破坏性软件

尽管因误输入命令和其他原因导致的用户错误可能会考验你的耐心，但无论是有意还是由于逻辑错误而破坏数据的软件可能更麻烦。本节讨论了一些防止破坏性软件破坏数据的措施。

### 病毒

与 Windows 不同，用户可以完全控制整个系统，Linux 系统内置了安全功能。这使得恶意程序的传播变得更加困难，这也是 Linux 系统上病毒如此之少的关键原因之一。病毒是一种附加到另一个可执行文件的程序，并在执行时尝试将其自身传播到其他可执行文件。除了这种行为外，病毒通常还会执行其他操作，范围从良性，如显示消息，到破坏性，如破坏你的分区表内容。

### 特洛伊木马

另一种恶意程序被称为特洛伊木马。特洛伊木马是一种伪装成另一个程序的程序。特洛伊木马可能被设计成像它所替换的程序一样工作，并执行诸如捕获密码并将其发送给特洛伊木马创建者之类的操作。它也可能执行更具破坏性的操作，如删除关键文件或目录。特洛伊木马的破坏性取决于谁执行了该程序。

### 蠕虫

蠕虫是一种利用系统弱点将自身传播到其他系统的程序。蠕虫通常被设计为寻找网络中的弱点，通常并不具有破坏性。蠕虫的问题在于，它们可能导致服务拒绝，因为它们试图移动到其他系统。
