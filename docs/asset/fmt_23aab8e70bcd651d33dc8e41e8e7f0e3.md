
`system.log=14`

# Anything with a duration of zero is not rotated.

`wtmp=0`

```
清单 6-13：rotatelogs 脚本的示例配置文件
```

## 工作原理

这个脚本的核心，当然也是最棘手的部分，是标注 1 处的 `find` 语句。`find` 语句创建了一个循环，返回 `/var/log` 目录中所有大小大于零个字符、名称中不包含数字、不以点开头（尤其 OS X 会向该目录倾倒大量名称奇怪的日志文件——这些文件都需要跳过）且不以 `conf` 结尾（出于显而易见的原因，我们不希望轮换掉 `rotatelogs.conf` 文件）的文件。`maxdepth 1` 确保 `find` 不会进入子目录，而最末尾的 `sed` 调用会移除匹配结果中所有开头的 `./` 序列。

> 注意
> 偷懒是好事！`rotatelogs` 脚本展示了 shell 脚本编程中的一个基本概念：避免重复工作的价值。与其让每个日志分析脚本都去轮换日志，不如由一个日志轮换脚本集中处理该任务，并让修改变得容易。

## 运行脚本

该脚本不接受任何参数，但会打印哪份日志正在被轮换及其原因等消息。它还应该以 `root` 身份运行。

## 运行结果

`rotatelogs` 脚本使用起来很简单，如清单 6-14 所示，但要注意，根据文件权限的不同，它可能需要以 `root` 身份运行。

```
$ sudo rotatelogs

ftp.log's most recent backup is more recent than 30 days: skipping

Rotating log lastlog (using a 14 day schedule)

... lastlog -> lastlog.1

lpr.log's most recent backup is more recent than 30 days: skipping
```

清单 6-14：以 `root` 身份运行 `rotatelogs` 脚本以轮换 `/var/log` 中的日志

请注意，在这次调用中，只有三个日志文件符合指定的 `find` 条件。其中，根据配置文件中的时长值，只有 `lastlog` 最近没有足够频繁地备份。然而，再次运行 `rotatelogs`，则不会执行任何操作，如清单 6-15 所示。

```
compress="bzip2"          # Change to your favorite compression app.

inclist="/tmp/backup.inclist.$(date +%d%b%Y)"

output="/tmp/backup.$(date +%d%b%Y).bz2"

tsfile="$HOME/.backup.timestamp"

btype="incremental"       # Default to an incremental backup.

noinc=0                     # And here's an update of the timestamp.

trap "/bin/rm -f $inclist" EXIT

usageQuit()

{

    cat << EOF >&2

Usage: $0 [-o output] [-i|-f] [-n]

-o lets you specify an alternative backup file/device,

-i is an incremental, -f is a full backup, and -n prevents

updating the timestamp when an incremental backup is done.

EOF

    exit 1

}

######## Main code section begins here ########

while getopts "o:ifn" arg; do

    case "$opt" in

        o ) output="$OPTARG";    ;;  # getopts automatically manages OPTARG.

        i ) btype="incremental"; ;;

        f ) btype="full";        ;;

        n ) noinc=1;              ;;

        ? ) usageQuit            ;;

    esac

done

shift $(( $OPTIND - 1 ))

echo "Doing $btype backup, saving output to $output"

timestamp="$(date '+%m%d%I%M')"  # Grab month, day, hour, minute from date.

                                 # Curious about date formats? "man strftime"

if [ "$btype" = "incremental" ] ; then

    if [ ! -f $tsfile ] ; then

        echo "Error: can't do an incremental backup: no timestamp file" >&2

        exit 1

    fi

    find $HOME -depth -type f -newer $tsfile -user ${USER:-LOGNAME} | \

    pax -w -x tar | $compress > $output

    failure="$?"

else

    find $HOME -depth -type f -user ${USER:-LOGNAME} | \

    pax -w -x tar | $compress > $output

fi

if [ "$noinc" = "0" -a "$failure" = "0" ] ; then

touch -t $timestamp $tsfile

fi

exit 0
```

Listing 6-16: 备份脚本

## How It Works

对于完整系统备份，① 和 ② 处的 `pax` 命令完成所有工作，将其输出通过管道传递给压缩程序（默认使用 `bzip2`），然后写入输出文件或设备。增量备份稍微复杂一些，因为标准版本的 `tar` 不包含任何修改时间测试，而 GNU 版本的 `tar` 则有。 自上次备份以来被修改的文件列表由 `find` 构建并保存在 `inclist` 临时文件中。该文件模仿 `tar` 输出格式以提高可移植性，然后直接馈送给 `pax`。

何时为备份标记时间戳是一个容易出错的区域，许多备份程序都会搞砸，通常将“上次备份时间”标记为备份程序完成备份时，而不是开始时。将时间戳设置为备份完成的时间可能存在问题，如果在备份过程中有文件被修改，随着单个备份所需时间变长，这种情况发生的可能性会更大。在这种情况下被修改的文件，其最后修改日期会早于时间戳日期，因此下次运行增量备份时将不会被备份，这很糟糕。

但请稍等，因为将时间戳设置为备份开始之前也是错误的：如果备份因某种原因失败，就无法撤销更新后的时间戳。

这两种问题都可以通过在备份开始前保存日期和时间（保存在 `timestamp` 变量中），但仅在备份成功后才使用 `touch` 的 `-t` 标志将 `$timestamp` 的值应用到 `$tsfile` 来避免。微妙吧？

## Running the Script

此脚本有多个选项，全部可以忽略以执行默认的增量备份，该备份基于自上次运行脚本以来被修改的文件（即自上次增量备份的时间戳以来）。启动参数允许你指定不同的输出文件或设备（`-o output`），选择完整备份（`-f`），主动选择增量备份（`-i`）即使它是默认值，或在增量备份的情况下阻止时间戳文件被更新（`-n`）。

## The Results

备份脚本不需要任何参数且运行简单，如 Listing 6-17 所述。

```
$ backup

Doing incremental backup, saving output to /tmp/backup.140703.bz2
```

清单 6-17：运行备份脚本不需要参数并将结果打印到屏幕。

正如你所预期的那样，备份程序的输出并不十分引人注目。但由此产生的压缩文件足够大，足以显示其中包含大量数据，如清单 6-18 所示。

```
$ ls -l /tmp/backup*

-rw-r--r-- 1 taylor wheel 621739008 Jul 14 07:31 backup.140703.bz2
```

清单 6-18：使用 `ls` 显示备份文件

## 52 备份目录

与备份整个文件系统的任务相关的是以用户为中心的任务，即对特定目录或目录树进行快照。清单 6-19 中的简单脚本允许用户为归档或共享目的创建指定目录的压缩 `tar` 归档。

### 代码

```
#!/bin/bash
```
