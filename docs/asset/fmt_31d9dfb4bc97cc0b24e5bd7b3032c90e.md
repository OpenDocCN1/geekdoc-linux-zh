
$ dump 2usfd 2300 /dev/rmt1 /dev/disk4 # 对通过 /dev/diskld 的文件系统执行级别 2 备份，使用 9 2300 英尺 (s) 磁带驱动器 /dev/rmt1，密度为 6250 BPI (d)，然后更新文件 /etc/dumpdates

```bash
$ dump 3usfd 2300 6250 /dev/rmt20 /dev/disk4 # 对通过 /dev/diskld 的文件系统执行级别 3 备份，使用 9 道 2300 英尺 (s) 磁带驱动器 /dev/rmt20，密度为 6250 BPI (d)，然后更新 /etc/dumpd (u)。
```

```bash
$ dump lusaf 1422 /dev/rfd0a /dev/rsd0
```

```bash
# 在 Sun 系统上对通过 /dev/rsd0 访问的文件系统到磁盘驱动器 /dev/rfd0a 执行级别 1 备份，然后更新文件 /etc/dumpd
```

```bash
$ dump 4W 6250 /dev/disk1
```

```bash
# 不备份任何文件系统。它将打印所有文件系统的完整列表，指示每个文件系统上次备份的时间、备份级别，以及是否需要在该级别进行备份（当指定 w 选项时，将忽略级别以外的所有其他选项）。
```

## 12.4.4 示例

两个真实的示例，一个来自 Sun OS 4.1.x（BSD 代表），另一个来自 Solaris 2.x（System V 代表），两个 Unix 变体均源自同一制造商 Sun Microsystems，且两个示例都与在单个磁带上备份多个文件系统有关。在第一个示例中，两个文件系统备份到 150 MB 1/4 英寸带盒（QIC-150）。在第二个示例中，五个文件系统备份到 2GB DAT 磁带。分别使用了 BSD 类的 `dump` 命令和 `udump`。在两种情况下，都创建了适当 Bourne 脚本来执行备份。这样就消除了错误的可能，因为脚本之前经过了测试和验证。完整的备份过程存储在名为 `dump.log` 的文件中。

以下是 Solaris 2.x 上对应的脚本 `backup_system`：

```bash
$ /usr/local/bin/backup_system

#!/bin/sh
```

```bash
# 在 ATLAS 上备份文件系统的脚本

# (这是 Solaris 2.6 UNIX 且使用了 "ufdump")。

# 备份两个磁盘驱动器上的文件系统

# (c0t3d0 和 c0t2d3)。

echo "Backing filesystems on ATLAS:" /tmp/dump.log

date >> /tmp/dump.log

echo "Verifying the tape dump..." /tmp/dump.log

/bin/mem -f /dev/rmt 0 status >> /tmp/dump.log 2>&1

echo "Rewinding the tape..." /tmp/dump.log

/bin/mem -f /dev/rmt 0 rewind >> /tmp/dump.log 2>&1

echo "Starting backup..." /tmp/dump.log

/bin/ufdump 0ubf 96 /dev/rdsk/c0t3d0s >> /tmp/dump.log 2>&1

echo "Dumping filesystem..." /tmp/dump.log

/bin/ufdump 0ubf 96 /dev/rdsk/c0t3d06 >> /tmp/dump.log 2>&1

echo "Dumping /home filesystem..." /tmp/dump.log

/bin/ufdump 0ubf 96 /dev/rdsk/c0t3d07 >> /tmp/dump.log 2>&1

echo "Dumping application filesystem..." /tmp/dump.log

/bin/ufdump 0ubf 96 /dev/rdsk/c0t2d30 >> /tmp/dump.log 2>&1

echo "Dumping software filesystem..." /tmp/dump.log

/bin/ufdump 0ubf 96 /dev/rdsk/c0t2d06 >> /tmp/dump.log 2>&1

echo "Dumping filesystem..." /tmp/dump.log

/bin/mem -f /dev/rmt 0 status >> /tmp/dump.log 2>&1

echo "Dumping..." /tmp/dump.log

echo "Rewinding the tape..." /tmp/dump.log

/bin/mem -f /dev/rmt 0 rewind >> /tmp/dump.log 2>&1

echo "D backup..." /tmp/dump.log
```

SunOS 上的脚本结构是相同的，唯一的区别是 `dump` 命令（而非 `udump`），应用如下：

```bash
$ dump /usr/local/bin/backup_system

#!/bin/sh

# 在 ATLAS 上备份文件系统的脚本

# (这是 Solaris 2.6 UNIX 且使用了 "ufdump")。

# 备份两个磁盘驱动器上的文件系统

# (c0t3d0 和 c0t2d3)。

echo "Backing filesystems on ATLAS:" /tmp/dump.log

date >> /tmp/dump.log

echo "Verifying the tape dump..." /tmp/dump.log

/bin/mem -f /dev/rmt 0 status >> /tmp/dump.log 2>&1

echo "Rewinding the tape..." /tmp/dump.log

/bin/mem -f /dev/rmt 0 rewind >> /tmp/dump.log 2>&1

echo "Starting backup..." /tmp/dump.log

/bin/ufdump 0ubf 96 /dev/rdsk/c0t3d0s >> /tmp/dump.log 2>&1

echo "Dumping filesystem..." /tmp/dump.log

/bin/ufdump 0ubf 96 /dev/rdsk/c0t3d06 >> /tmp/dump.log 2>&1

echo "Dumping /home filesystem..." /tmp/dump.log

/bin/ufdump 0ubf 96 /dev/rdsk/c0t3d07 >> /tmp/dump.log 2>&1

echo "Dumping application filesystem..." /tmp/dump.log

/bin/ufdump 0ubf 96 /dev/rdsk/c0t2d30 >> /tmp/dump.log 2>&1

echo "Dumping software filesystem..." /tmp/dump.log

/bin/ufdump 0ubf 96 /dev/rdsk/c0t2d06 >> /tmp/dump.log 2>&1
```

对应的日志文件 `/tmp/dumpit.log` 内容：

```bash
$ cat /tmp/dumpit.log

Wed Nov 7 16:37:38 1998

Backing filesystems on ATLAS

Verifying the drive...

Archive QIC-150 tape:

sense(0x0)=no residual = 0 retries = 0

file no=0 block no=0

Rewinding the Tape...

Starting backup...

Dumping filesystem...

Date of this level 0 dump: Wed Nov 7 16:43:12 1998

Dumping /dev/rds0 (/) to /dev/nrst0
```

相应的消息是命令本身的一个逻辑部分，尽管驱动程序本身独立执行了回带。今天，磁带不再需要回带，但即使在使用“回带”设备时，此消息仍然存在。

检查第一个日志文件，我们发现关于磁带卷绕的混淆 DUMP 消息已不存在。引入了 `fsdump` 命令，所有之前的备份都得到了修复。

另一个示例说明了用户数据的归档，在本例中是实验性核磁共振（NMR）数据。用户将数据保存在目录下的单独子目录；所有数据都应定期压缩并保存到 QIC-150 磁带上。

再次创建了适当脚本文件 `backup_data.sh`；使用了 `tar` 命令进行数据归档（不需要对整个文件系统进行备份）。实现的目录和文件名与此实际情况对应。（注释已用**粗体**标记，以便更具可读性。）

```bash
$ cat /usr/CM/CMcombs/backup_data.sh

#!/bin/sh

#

######################################################################

# 使用 tape 命令：

# /usr/CM/CMcombs/backup_data

# 日志文件位于：/home/backup_data.log

# 磁带类型：tar -tf /dev/rst0

######################################################################

# 备份的账户目录

cd /home

# 预防性删除已用文件

rm backup_data.log 2>/dev/null

rm dirs 2>/dev/null

rm nmrusers 2>/dev/null

#

# 指定用户家目录

ls > dirs

# 提取 NMR 数据的目录

for dir in 'cat dirs'

do

  if [ -d $dir/data ]; then

    echo "$dir/data;" >> nmrusers

  fi

done

# 将 users/data 归档到磁带

date >> /home/backup_data.log

echo "注意使用 tar 命令!" >> /home/backup_data.log

echo "" >> /home/backup_data.log

tar -cvf /dev/rst0/home/nmrusers >> /home/backup_data.log

#

# 删除临时文件

rm /home/dirs

rm /home/nmrusers
```

## 12.5 从备份恢复文件

所有之前讨论的备份设施都有相应的文件恢复设施。其中核心是 `restore` 命令。与 `dump` 命令类似，`restore` 也源自 BSD UNIX，但最终出现在 System V 平台上。同样，它有时有一个别名 `ufsstore`，但功能上是相同的。

### 12.5.1 restore 命令

与备份一样，`restore` 命令有多种实现，或者说 `restore` 命令在不同的 UNIX 版本和发行之间有所不同。以下是简要回顾。

### 12.5.1.1 SVR3 restore 命令

另一个简短的历史回顾：SVR3 restore 命令是所述 SVR3 备份命令的补充。它是过时的，这里提到它的唯一理由是为了教学目的，以展示其连续性。SVR3 restore 命令具有以下格式：

```
restore options file_list
```

其中

- `file_list`：要恢复的文件列表。允许在引号中使用通配符。
- `options`：一个或多个可用的选项。

选项如下：

| 选项 | 含义 |
| --- | --- |
| `-c` | 恢复所有文件（完整恢复） |
| `-I` | 列出磁带/软磁盘的内容（可用于验证备份） |
| `-o` | 恢复时覆盖现有文件（默认不恢复现有文件） |
| `-d res_dev` | 从 restore 指定设备_dev |
| `-t` | 指明 res_dev 是磁带设备 |

这里有几个示例：

```
# restore -c # 从默认软驱器中的软磁盘恢复所有文件
# restore -d /dev/rmc/c00 -t -o "home/username/data/*.dat"
# 从第一个磁带驱动器的磁带中恢复 /home/username/data 目录下选定的 *.dat 文件，并覆盖现有文件
```

#### restore/ufs 命令

BSD 风格的 `restore` 命令从用 BSD–dump 命令制作的备份磁带中恢复文件。该命令也支持其他 UNIX 变体，包括某些 SVR4 版本（有时重命名为 ufs）。`restore/ufs` 命令可以恢复单个文件、多个目录或整个文件系统。要恢复整个文件系统，必须遵守不同级别的备份顺序：首先是最完整的转储（level 0），然后是 level 1 备份，依此类推。因此，为了完整恢复文件系统，系统管理员可能希望创建并挂载一个干净空的文件系统，将该文件系统的挂载点作为当前工作目录，然后使用 `restore/ufs` 命令将磁带读回此目录。

如果文件系统是从完整（level 0）转储加一个或多个增量转储恢复的，那么在 level 0 备份之后删除的所有文件都将再次恢复；增量转储不会跟踪已删除的文件。

在任何完整恢复后，都应该重新进行完整（level 0）备份，以确保磁盘（磁盘）和磁带上 inode 编号的一致性。`dump/fsdump` 命令复制 inode 编号，而 `restore/ufsrestore` 命令在恢复文件时按顺序分配 inode 编号。

`restore/ufsrestore` 命令具有以下形式：

```
restore options arguments [files_and_dirs]
```

或者，：

```
ufsrestore arguments [files_and_dirs]
```
