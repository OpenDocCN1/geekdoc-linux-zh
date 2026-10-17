
相关目录都在`/etc`中，逻辑上命名为`cron.hourly`、`cron.daily`、`cron.weekly`和`cron.monthly`。这种方法有趣之处在于你不再需要担心时间说明符——如果它在`cron.daily`目录中，它将由`crond`每天运行一次。

### 1. 让我们看看这些目录中有什么：

```
# ls -R /etc/cron.*
/etc/cron.d:
  sysstat

/etc/cron.daily:
  00-logwatch  0anacron  makewhatis.cron  slocate.cron  tmpwatch
  00webalizer  logrotate  rpm  sysstat

/etc/cron.hourly:

/etc/cron.monthly:
  0anacron

/etc/cron.weekly:
  0anacron  makewhatis.cron
```

`/etc/cron.d`中的条目采用常规`crontab`行格式；它们只是让你避免拥有一个非常大的`crontab`文件。否则，所有其他文件都是简单的`shell`脚本。

### 2. 你现在应该很容易理解`/etc/cron.d/sysstat`文件指定了什么，以及`cron`系统应在何时运行它：

```
# more /etc/cron.d/sysstat
# run system activity accounting tool every 10 minutes
*/10 * * * * root /usr/lib/sa/sa1 1 1
```

这指定每10分钟运行一次`sa1`。

![](img/5ced0c78d748bd190e9027e5549a3622_309_0.png)

> 请注意注释的使用如何帮助你理解正在发生的事情。作为一般规则，你应该始终尝试在`crontab`文件中的每一行之前加上注释，解释你期望的频率。

### 3. 每周`cron`作业是我们开始的好地方，所以让我们看看`Red Hat Linux`中包含的默认文件：

```
# cd /etc/cron.weekly
# more *
::::::::::::::
0anacron
::::::::::::::
#!/bin/sh
#
# anacron's cron script
#
# This script updates anacron time stamps. It is called through run-parts
# either by anacron itself or by cron.
#
# The script is called '0anacron' to assure that it will be executed
# _before_ all other scripts.

anacron -u cron.weekly
::::::::::::::
makewhatis.cron
::::::::::::::
#!/bin/bash

LOCKFILE=/var/lock/makewhatis.lock

# the lockfile is not meant to be perfect, it's just in case the
# two makewhatis cron scripts get run close to each other to keep
# them from stepping on each other's toes. The worst that will

```

# happen is that they will temporarily corrupt the database...

[ -f $LOCKFILE ] && exit 0

trap "rm -f $LOCKFILE" EXIT

touch $LOCKFILE

makewhatis -w

exit 0

```

与这些管理脚本典型的情况一样，这两个示例本质上都只有一行长。第一个`0anacron`调用`anacron -u cron.weekly`，而第二个`makewhatis.cron`每周使用`makewhatis -w`重建`whatis`数据库（由`man -k`使用）。

### 4. 每天的脚本更有趣，而且数量更多，所以让我们看看是否有任何不寻常或特别值得称道的：

```
# wc -l *
```

| 行 | 文件 |
|-------|------|
| 691 | 00.logwatch |
| 8 | 00webalizer |
| 12 | 0anacron |
| 3 | logrotate |
| 13 | makewhatis.cron |
| 4 | rpm |
| 3 | slocate.cron |
| 5 | sysstat |
| 7 | tmpwatch |
| 746 | total |

`logwatch`脚本长达691行，相当惊人。否则，你可以看到这些脚本都相当简短。其中一些提供了有趣的技术：

```
# cat 00webalizer

#!/bin/bash

# update access statistics for the web site

if [ -s /var/log/httpd/access_log ] ; then

/usr/bin/webalizer

fi
```

这是管理员脚本中常见的构造——如果特定数据文件存在，则运行分析它的程序。在这种情况下，它会检查`Web`服务器（`httpd`）是否收到任何访问。如果有，`webalizer`将生成一些基础的日志文件分析。

```
# cat slocate.cron

#!/bin/sh

renice +19 -p $$ >/dev/null 2>&1

/usr/bin/updatedb -f "nfs,smbfs,ncpfs,proc,devpts" -e "/tmp,/var/tmp,/usr/tmp,/afs,/net"
```

这是简洁脚本的绝佳示例，由真正理解`shell`脚本细微差别的人编写。`renice`命令通过将其设置为`+19`，尽可能降低其自身`shell`（请记住`$$`是`shell`的`PID`）的优先级。现在系统上的每个其他任务都比这个`shell`脚本更重要。下一行通过启动`updatedb`执行实际工作，后者重建`locate`文件名数据库。

### 5. 再举一个例子，一个相当巧妙地使用`shell`脚本和通过模式进行文件名扩展的用法。

```
# cat tmpwatch

/usr/sbin/tmpwatch 240 /tmp

/usr/sbin/tmpwatch 720 /var/tmp

for d in /var/{cache/man,catman}/{cat?,X11R6/cat?,local/cat?}; do

  if [ -d "$d" ]; then

    /usr/sbin/tmpwatch -f 720 $d

  fi

done
```
