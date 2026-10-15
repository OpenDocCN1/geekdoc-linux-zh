

## 4.2 备份相关提示

某些文件和目录应独立于所使用的备份策略进行备份。它们不一定写入另一备份系统，而是存储在可访问的位置，以备需要时使用。

### 4.2.1 tar 重要文件

每个 *NIX 系统都使用在其生命周期内会发生变化的配置文件。如果系统需要重新安装，这些文件必须被复制回来。如果其中一个文件损坏或被覆盖，则需要尽快用可用副本替换它。

其中一些文件在某些系统上用于特殊目的；其他文件在每个 *NIX 系统上同等重要。清单 4.1 中显示的脚本将这些文件的副本存储在目录中，然后该目录被写入 tar 归档以供存储。

### 清单 4.1 备份重要文件的脚本

```
#!/usr/bin/sh
# $Id: backup_conf.sh,v 1.1 2004/08/18 11:15:26 root Exp root $
########################################
#
#       file:          backup_conf.sh
#
#       purpose:       backup important files to
#                      directory and tar it
#
#       author:        Erik Keller
#
#       parameters:    none
#
########################################

# Variables
SYSNAME=`uname -n`
DESTDIR=/.HO/backupconf
TODAY=`date '+%Y_%m_%d'`

# get the right tar (needed in Solaris only)
if [ -x /opt/sfw/bin/tar ]
then
    TAR=/opt/sfw/bin/tar
    TAR_OPTS=czf
    TAR_EXT=tar.gz
else
    TAR=/usr/bin/tar
    TAR_OPTS=cf
    TAR_EXT=tar
fi

# Files to backup
FILES="
/etc/resolv.conf
/etc/nsswitch.conf
/etc/cgroup
/etc/inet/hosts
/etc/inet/inetd.conf
/etc/logadm.conf
/etc/syslog.conf
/etc/system
/etc/vfstab
"

# Directories to backup
DIRS="
/etc/init.d
/etc/rc0.d
/etc/rc1.d
/etc/rc2.d
/etc/rc3.d
/etc/rcS.d
/etc/default
/etc/ssh
"

# function to copy the files in $FILES
copy_files()
{
        for FILE in $FILES
        do
                if [ -f $FILE ]
                then
                        DESTFILE=`echo $FILE | tr '/' '_'`
                        cp $FILE $DESTDIR/$SYSNAME/$SYSNAME.$DESTFILE
                        #echo $DESTDIR/$SYSNAME/$SYSNAME.$DESTFILE
                fi
        done
}

# function to copy the directories in $DIRS
copy_directories()
{
    for DIR in $DIRS
    do
        if [ -d $DIR ]
        then
            DESTFILE=`echo $DIR | tr '/' '_'`
            cp -r $DIR $DESTDIR/$SYSNAME/$DESTFILE
        fi
    done
}

# function to create the tar archive
make_tar()
{
    cd $DESTDIR
    TAR $TAR_OPTS $SYSNAME.$TODAY.$TAR_EXT $SYSNAME
}

# function to check if the directory structure is in place
dircheck()
{
    if [ ! -d $DESTDIR ]
    then
        mkdir -p $DESTDIR
    fi

    if [ ! -d $DESTDIR/$SYSNAME ]
    then
        mkdir $DESTDIR/$SYSNAME
    fi
}

# main program
dircheck
copy_files
copy_directories
make_tar

# EOF
```

脚本定义了变量 `$SYSNAME`、`$DESTDIR` 和 `$TODAY`。`$SYSNAME` 包含系统名称，`$DESTDIR` 为文件应复制到的目录路径。后者理想情况下应指向另一个分区上的目录，或更好的是另一块硬盘。你应牢记这些文件包含有价值的信息，可能使入侵者能够破坏系统。它们应存储在只有超级用户可访问的位置。`$TODAY` 包含当前日期，用作生成的 tar 归档名称的一部分。这样归档不会互相覆盖，从而允许你创建某种配置历史。

选择使用哪个 `tar` 程序是 Solaris 特有的。如果脚本部署在其他 *NIX 系统上，你可以使用该系统上安装的 `tar` 程序的路径和名称。如果系统包含多个 `tar` 程序，请自定义示例函数以确保创建一致的归档。

变量 `$FILES` 和 `$DIRS` 包含所有要备份的文件和目录。它们因系统而异。例如，如果使用 Apache Web 服务器，则必须将包含其配置文件的目录添加到 `$DIRS` 变量中。对于特定系统重要的其他配置文件也是如此。

`copy_files()` 函数测试相应文件是否存在。如果存在，它会复制文件并按如下方式更改文件名：例如 `/etc/syslog.conf` 变为 `unixhost_etc_syslog.conf` 等等。这使你能够识别文件最初用于的系统。测试文件是否存在允许你在相似系统上部署脚本而无需大量自定义。如果文件不存在，则不会被复制，也不会有错误消息。此系统按预期工作的一个要求是文件列表中没有拼写错误。这不应成为问题，因为脚本在部署前无论如何都应经过彻底测试。

`copy_directories()` 函数或多或少模仿 `copy_files()`，但不会在目录名中添加系统名称。`$DESTDIR/$SYSNAME` 中保存的目录以下划线 `_` 开头。

`make_tar` 函数创建 tar 归档。将归档的创建封装在函数中似乎并非必要，但这样做可以更轻松地在以后扩展脚本。

`dircheck()` 函数测试 `$DESTDIR` 中使用的目录结构是否存在，并在测试失败时创建目录。

真正的脚本在注释 `# main program` 之后开始；所有函数按出现顺序执行。如果通过 cron 执行脚本部署，写入日志文件是个好主意。大多数 *NIX 系统为此目的使用 `logger` 程序。它用于向 syslogd 进程发送消息。你可以在脚本末尾简单添加以下行：

```
logger -p user.crit $0 done.
```
