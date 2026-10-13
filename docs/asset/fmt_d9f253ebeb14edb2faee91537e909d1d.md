
当系统首次启动时，它处于运行级别 1。它首先执行`/sbin/rc1.d`目录中的所有停止脚本，然后执行该目录中的所有启动脚本。一旦运行级别 1 对应的目录中的所有脚本都已执行，就使用参数`start`执行运行级别 2 对应的目录中的脚本，然后执行运行级别 3 中的脚本。当运行级别 3 中的所有脚本执行完毕后，系统即可供一般使用。

当系统关机并断电或停止时，`/sbin/rc5.d`目录中的脚本将被执行。当系统重启时，`/sbin/rc6.d`目录中的脚本将被执行。

### 平台差异

除了 BSD 之外，UNIX 厂商 readily 采用了 AT&T 的初始化基础设施。BSD 仍继续使用基于文件`/etc/rc`和`/etc/rc.local`的系统。

Hewlett-Packard 在 HP-UX 10.0 中采用了它，并进行了轻微修改使用。在 HP-UX 中，init 脚本仍存储在目录`/sbin/init.d`中，运行级别目录仍命名为`/sbin/rc?.d`，但启动和停止脚本具有三位数字`XXX`或`YYY`，而不是仅两位数字`XX`或`YY`。因此在 HP-UX 上，`YYY`应等于`1000 - XXX`。

Sun Microsystems 在 Solaris 2.0（SunOS 5.0）中采用了它并根据其需求进行了修改。在 Solaris 中，init 脚本存储在目录`/etc/init.d`中，运行级别目录命名为`/etc/rc?.d`。

Linux 也采用了修改后的 AT&T 风格初始化。在 Linux 中，init 脚本存储在`/etc/rc.d/init.d`中，运行级别目录命名为`/etc/rc.d/rc?.d`。Linux 还更改了与运行级别 5 相关的含义；而不是使用此运行级别来停止系统并断电，它被用于启动图形窗口环境（X11）所需的进程。Linux 也保留了一些 BSD 的痕迹，因为它仍使用文件`rc.local`（已重新定位到目录`/etc/rc.d`）。

> **BSD 可能最终采用 System V 初始化**
> 
> 尽管 BSD 在十多年里一直避免采用 System V 风格的初始化，但变革的迹象正在出现。一个名为 NetBSD rc.d System 的倡议由 NetBSD 基金会在 2001 年夏季推出。有关该倡议的更多信息可在以下论文中找到：
> 
> http://www.cs.rmit.edu.au/~luken/papers/rc.d.pdf

### 开发 Init 脚本

如前所述，init 脚本的基本接口是`script [ start | stop ]`

你将首先为安全外壳守护进程（SSH）创建一个脚本，实现此接口，然后添加若干改进以增强脚本的功能。完成脚本后，本节将介绍将脚本适配到不同程序所需的更改。

为本节目的，假设你的 init 脚本名为`sshd`且存储在`/sbin/init.d`中。启动脚本的实际位置取决于系统，如前所述。

#### 基础脚本

下面的脚本实现了基本`start`和`stop`接口：

```
#!/bin/sh

PGM=/usr/local/sbin/sshd

PGM_OPTS=

case "$1" in

  start) $PGM $PGM_OPTS ;;

  stop) /bin/ps -ef | grep "$PGM" | grep -v grep | \
        awk '{ print $2; }' | xargs kill 2> /dev/null

        ;;

esac

exit 0
```

在脚本开头，你定义了两个变量`$PGM`和`$PGM_OPTS`。变量`$PGM`包含要启动程序的完整路径（本例中为`/usr/local/sbin/sshd`）；而变量`$PGM_OPTS`包含可能需要指定给程序的任何额外选项或参数。

变量定义之后跟随的`case`语句会评估提供给脚本的参数。如果参数为`start`，则存储在`$PGM`中的程序按如下方式执行：`$PGM $PGM_OPTS`

如果参数为`stop`，则程序使用以下复合命令停止：`/bin/ps -ef | grep "$PGM" | grep -v grep | awk '{ print $2; }' | xargs kill 2> /dev/null`

基本上，此命令使用`grep`在`ps`的输出中查找所有与存储在`$PGM`中的字符串匹配的条目。然后它忽略同时包含`$PGM`和`grep`的任何条目。然后它使用`awk`提取这些进程的进程 ID 并使用`kill`终止这些进程

尽管基础脚本可用，但仍有一些问题需要解决才能使其更易用：

- 脚本在存储在`$PGM`中的程序不存在或不可执行时没有错误报告。
- 脚本在存储在`$PGM`中的程序已运行时没有错误报告。
- 如果向脚本提供无效参数（或未提供参数），则不会提供使用信息。

为了解决第一个和第二个问题，你可以将`case`语句的`start`子句更改为以下内容：

```
start)

if [ ! -x "$PGM" ] ; then

    echo "Error: Not executable: $PGM" 1>&2

    exit 1

fi

RUNNING=`/bin/ps -ef | grep "$PGM" | grep -v grep | head`

if [ -n "$RUNNING" ] ; then

    echo "Error: Already running: $PGM" 1>&2

    exit 1

fi

"$PGM" $PGM_OPTS

;;
```

如你所见，`start`子句现在包含两个`if`语句来执行必要的错误检查。首先，你使用`-x`文件测试选项验证程序是否可执行。如果不可执行（或不存在），则报告错误消息并退出脚本。否则，脚本继续进行下一步错误检查。

为了检查程序是否已在运行，你使用以下复合命令：

`RUNNING=`/bin/ps -ef | grep "$PGM" | grep -v grep | head``

如果程序已在运行，则变量`RUNNING`的值将包含至少一个程序实例的`ps`输出。否则`RUNNING`将为空。你使用`-z`选项检查变量`RUNNING`；如果它不为空，则报告错误消息。

`start`子句的最后一部分保持不变；你只需按如下方式执行程序：

```
"$PGM" $PGM_OPTS
```

为了解决第三个问题，你只需向`case`语句添加一个默认子句：

```
* ) echo 'Usage: $0 [ start | stop ]' ; ;
```

加入这些更改后，脚本现在如下所示：

```
#!/bin/sh

PGM=/usr/local/sbin/sshd

PGM_OPTS=

case "$1" in

start)

  if [ ! -x "$PGM" ] ; then

    echo 'Error: Not executable: $PGM' 1>&2

    exit 1

  fi

  RUNNING=`/bin/ps -ef | grep "$PGM" | \
    grep -v grep | head -1`

  if [ -n "$RUNNING" ] ; then

    echo 'Error: Already running: $PGM' 1>&2

    exit 1

  fi

  "$PGM" $PGM_OPTS

  ;;

stop)

  /bin/ps -ef | grep "$PGM" | grep -v grep | \
  awk '{ print $2 }' | xargs kill 2>/dev/null

  ;;

*) echo 'Usage: $0 [ start | stop ]' 

  exit 1

  ;;

esac

exit 0
```

#### ps 的问题

此脚本的一个问题在于使用`ps`命令。如你可能从第 7 章“进程”中回忆到的，`ps`理解的选项在各系统间有所不同。此脚本使用了 Solaris 风格的`-ef`选项。Linux 和 BSD 系统并不总是支持这些选项，因此在这些系统上你需要改用`auxww`选项。此脚本应能够检测其运行的系统类型并相应地进行调整。

你可以使用`uname -s`命令检测系统类型，然后使用`case`语句修改`ps`命令中的选项：

```sh
case `uname -s` in
Linux|Darwin|BSD) PS="/bin/ps auxwx" ;;
*) PS="/bin/ps -ef" ;;
esac
```

此`case`语句评估`uname -s`命令的输出。如果输出为 Linux、Darwin（MacOS X）或某个版本的 BSD，则变量`ps`设置如下：

```sh
PS="/bin/ps auxwx"
```

否则它默认为 Solaris 风格的值：

```sh
PS="/bin/ps -ef"
```
