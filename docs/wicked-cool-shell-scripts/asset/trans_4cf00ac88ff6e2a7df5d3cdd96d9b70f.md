

当脚本接收到一个文件名作为参数时，它会尝试恢复该文件或目录（如果只有一个匹配项），或者显示一个可供恢复的候选项列表，并允许用户指定要恢复的已删除文件或目录的哪个版本。

## 运行结果

在不指定任何参数的情况下，脚本会显示已删除文件归档中的内容，如清单 2-8 所示。

```
$ unrm
Contents of your deleted files archive (sorted by date):
detritus          this is a test
detritus           garbage
```

> 清单 2-8：不带参数运行 unrm shell 脚本，列出当前可恢复的文件

当指定了一个文件名时，如果存在多个同名文件，脚本会显示有关该文件的更多信息，如清单 2-9 所示。

```
$ unrm detritus
More than one file or directory match in the archive:
1) detritus (size = 7688Kb, deleted = 11/29 at 10:00:12)
2) detritus (size = 4Kb, deleted = 11/29 at 09:59:51)
Which version of detritus should I restore ('0' to quit)? [1] : 0
unrm: Restore canceled by user.
```

> 清单 2-9：带单个参数运行 unrm shell 脚本，尝试恢复该文件

## 修改脚本

如果你使用这个脚本，请注意，如果没有控制或限制，已删除文件归档中的文件和目录将无限增长。为避免这种情况，可以在 cron 作业中调用 find 来清理已删除文件归档，使用 `-mtime` 标志来识别那些已经数周未动的文件。对于大多数用户来说，14 天的归档期可能已经足够，并且可以防止归档脚本占用过多磁盘空间。

既然提到了改进，这里有一些可以让这个脚本更用户友好的优化。考虑添加起始标志，比如 `-1` 表示恢复最新版本，`-0` 表示不额外删除文件的副本。你会添加哪些标志？它们又会如何简化处理流程？

## #17 记录文件删除操作

除了归档已删除的文件之外，你可能只想跟踪系统上发生的删除操作。在清单 2-10 中，使用 rm 命令删除文件的操作将被记录到一个单独的文件中，而不会通知用户。这可以通过将脚本用作包装器来实现。包装器的基本思想是它们位于实际 Unix 命令和用户之间，为用户提供单独使用原始命令无法获得的有用功能。

> 包装器是一个如此强大的概念，在阅读本书的过程中，你会一遍又一遍地看到它们出现。

### 代码

```
#!/bin/bash
# logrm--logs all file deletion requests unless the -s flag is used

removelog="/var/log/remove.log"

① if [ "$#" -eq 0 ] ; then
    echo "Usage: $0 [-s] list of files or directories" >&2
    exit 1
fi

② if [ "$1" = "-s" ] ; then
    # Silent operation requested ... don't log.
    shift
else
③   echo "$(date): $(USER): $0 $@" >> $removelog
fi

④ /bin/rm "$@"

exit 0
```

> 清单 2-10：logrm shell 脚本

### 工作原理

第一部分 ① 测试用户输入，如果未给出参数则生成一个简单的文件列表。然后在 ② 处，脚本测试参数 1 是否为 `-s`；如果是，则跳过记录删除请求。最后，时间戳、用户和命令被添加到 `$removelog` 文件 ③ 中，用户命令被静默传递给真正的 `/bin/rm` 程序 ④。

### 运行脚本

与其给这个脚本起一个像 logrm 这样的名字，安装包装程序的一种典型方式是将它打算包装的基础命令重命名，然后用原始命令的旧名称安装该包装器。然而，如果你选择这条路，请确保包装器调用的是新命名的程序，而不是它自己！例如，如果你将 `/bin/rm` 重命名为 `/bin/rm.old`，并将此脚本命名为 `/bin/rm`，那么脚本的最后几行需要修改，以便调用 `/bin/rm.old` 而不是它自己。

或者，你可以使用别名将标准 rm 调用替换为这个命令：

```
alias rm=logrm
```

无论哪种情况，你都需要对 `/var/log` 拥有写和执行权限，这可能不是你特定系统的默认配置。

### 运行结果

让我们创建几个文件，删除它们，然后检查删除日志，如清单 2-11 所示。

```
$ touch unused.file ciao.c /tmp/junkit
$ logrm unused.file /tmp/junkit
$ logrm ciao.c
$ cat /var/log/remove.log
Thu Apr 6 11:32:05 MDT 2017: susan: /tmp/central.log
Fri Apr 7 14:25:11 MDT 2017: taylor: unused.file /tmp/junkit
Fri Apr 7 14:25:14 MDT 2017: taylor: ciao.c
```

> 清单 2-11：测试 logrm shell 脚本

啊哈！注意在星期四，用户 Susan 删除了文件 `/tmp/central.log`。

### 修改脚本

这里存在一个潜在的日志文件所有权权限问题。要么 remove.log 文件对所有用户都可写，在这种情况下，用户可以用诸如 `cat /dev/null > /var/log/remove.log` 之类的命令清除其内容；要么它不对所有用户都可写，在这种情况下，脚本无法记录事件。你可以使用 setuid 权限——让脚本以 root 身份运行——这样脚本就能以与日志文件相同的权限运行。然而，这种方法有两个问题。第一，这真的是一个糟糕的主意！绝不要在 setuid 下运行 shell 脚本！通过使用 setuid 以特定用户身份运行命令，无论谁在执行该命令，你都可能给系统引入安全弱点。第二，你可能会遇到一种情况，即用户有权限删除他们的文件，但脚本却没有，而且由于 setuid 设置的有效 uid 会被 rm 命令本身继承，事情就会出错。当用户甚至无法删除自己的文件时，就会引发极大的混乱！

如果你使用的是 ext2、ext3 或 ext4 文件系统（Linux 通常如此），另一种解决方案是使用 chattr 命令为日志文件设置仅追加的文件权限，然后让它对所有用户可写而没有任何危险。还有一种解决方案是使用有用的 logger 命令将日志消息写入 syslog。使用 logger 记录 rm 命令非常简单，如下所示：

```
logger -t logrm "$(USER:-LOGNAME): $*"
```

