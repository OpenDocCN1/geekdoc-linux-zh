
| 1,000,000 | 70,000 | 3,086 | 99.691% | 0.309% | 0.5 | 51 |

| 1,000,000 | 75,000 | 2,981 | 99.702% | 0.298% | 0.5 | 50 |

| 1,000,000 | 80,000 | 2,887 | 99.711% | 0.289% | 0.5 | 48 |

![](img/a6b8fd6f7dfea65f9a1b7e4c40482932_250_0.png)

图 8.7 使用示例数据满足目标 IO。

# 运行进度

运行 Progress 数据库的典型过程通常不是一项全职工作。通常需要为数据库启动、备份和关闭脚本编写一些初始脚本。之后，大部分时间花在收集数据上，以确保你的系统获得最佳性能。许多基于 Progress 的系统运行多年，无需任何数据库管理员（DBA）的关注。

# 管理数据库

PSC 提供了简单的脚本用于启动、停止、监控和备份数据库。虽然这些脚本对于初始开发环境通常足够，但对于生产环境工作通常需要更复杂或定制化的方法。一个有用的第一步是创建一个小型环境脚本，将所有重要的 Progress 和应用程序相关的环境变量合并到一个脚本中，然后在需要的脚本中对其进行“点源”（dotted）或“source”。例如：

```
# 通用环境脚本
# 使用方法：
#
# /mnt/scripts/env

export TMP=/mnt/tmp
export MTH=`date` +%m
export DAY=`date` +%d
export LOGS=/mnt/logs/$MTH.DAY
export SRV=`uname`
export SCRIPTS=/mnt/scripts
export DLC=/opt/progress/dlc83b
export DNAME=/mnt/db/sports
```

## 标准消息例程

```
msg()
{
MSG=$1 ; shift
echo "$MSG" >> $LOGS/start.log
echo `date` "$MSG"

# 如果传递了额外的参数，则将消息邮件给
# 那些人员（名称可能是呼叫地址）

[ "$1" != "" ] &&
echo $SRV: `date` "$MSG" | mailx -s "$MSG" *
}
```

## 启动

较小的站点通常使用自动检测数据库状态并在第一个用户尝试访问时将其启动的脚本。有时它们甚至会在最后一个用户退出时自动将其关闭。虽然很方便，但这种方法有几个潜在的陷阱。此类脚本绝不应该删除 `.lk` 文件。如果 Prolog 告诉你有锁存在，你应该认真对待该信息并理解其原因。可能是另一个你未知的用户启动了合法的单用户会话（可能是为了进行数据库维护）。删除该 `.lk` 文件然后访问数据库将导致两组进程，它们可能会在感知不到另一组进程的情况下更新数据库——这种情况显然会导致灾难。

这种方法的另一个缺点是，在需要维护时很难获取数据库的独占访问。为了安全地访问数据库进行维护或恢复，良好的做法是这种方法，使用一个标记来限制用户，例如：

```
# 启动服务器
/mnt/scripts/env
```

```
# 启动并验证
strt()
{
CMD=$1
USR=$2
GTX=$3
WHO=$4

msg "启动: $1"
$CMD >> $LOGS
sleep 5

ps -fu | grep "$GTX" > /dev/null
if [ $? = "1" ]; then
msg "*** CMD 未启动" $WHO
exit 0
else
msg "+++ CMD 启动成功"
fi
}
```

```
# 创建日志目录
if [ ! -d $SLOGS ]; then
  mkdir $SLOGS
  chmod 777 $SLOGS
fi
```

`msg` "启动数据库"

```
msg "锁定用户 - 请等待" >$TMP/Lockout
echo "启动数据库" > $TMP/Lockout
chmod 644 $TMP/Lockout
rm -f $TMP_IS_UP
sleep 5

$DLC/bin/proshut DBNAME -by >> $LOGS/stop.log 2>&1 &
sleep 60

# 验证代理已关闭 - by 选项在有用户时并不保证关闭

ps | grep -pf $DBNAME > /dev/null

if [ $? = "0" ]; then
    msg "*** 未通过 BY 关闭" dba
    msg "*** 尝试使用 F 选项强制关闭"
    DLC/bin/proshut DBNAME -F >> $LOGS/stop.log 2>&1
fi

ps | grep -pf $DBNAME > /dev/null

if [ $? = "0" ]; then # 慌
    msg "*** 未通过 F 关闭" dba
    cp $DBNAME.1lk $LOGS.xxx
    exit 0
fi

msg "+++ 数据库文件已关闭"

# 将 .lk 文件移动到存档
mv $DBNAME.1lk $LOGS # 除非关闭正常发生...
```

### 备份

备份 Progress 数据库有两种基本方法。可以使用 Progress 提供的 `PROBKUP` 程序、外部备份程序（如 `tar` 或 `cpio`）或商业产品。正确备份在线数据库的唯一方法是使用 `PROBKUP`。外部备份在不先关闭数据库的情况下无法正确备份运行中的 Progress 数据库。一种优秀的 Progress 备份方法是结合两种方法：使用 `PROBKUP` 备份到磁盘，然后使用外部备份命令将磁盘文件拷贝到磁带。只要配置了足够的磁盘空间，这种方法有许多优点：

- 减少停机时间——备份到磁盘比备份到磁带快得多
- 恢复时间——在许多恢复场景中，拥有离线磁带备份可以节省时间，而且从磁盘而非磁带恢复的速度更快
- 额外的保护——备份越多越好
- 能够轻松将应用程序的非数据库元素合并到单个磁带中

#### 示例备份脚本：

```
if [ -f $TMP/User_Lockout ]; then

clear

cat $TMP/User_Lockout

sleep 30

msg **** Backup of active database??" dba

exit 0

```

# 继续备份...

```
msg **** Starting PROKUP of $DBNAME

DLC/prokup $DBNAME /mnt/dump/$DBNAME >> $LOGS/backup.log 2>&1 &

nmsg **** PROKUP of $DBNAME complete with status $?

tar cvf /mnt/dump/$DBNAME.bak >> $LOGS/backup.log 2>&1

msg **** Backup of $DBNAME complete with status $?

```

定期测试您的恢复程序至关重要，以确保创建了有效的备份，并且您的磁带上包含了您所需的所有内容。实现此点的最佳方法是恢复到另一台机器上。这可以验证整个过程和所有的介质。PEG 经常刊登一些不幸灵魂的故事，他们以为自己每晚都在备份，结果却发现根本没有任何恢复手段。不要加入他们的行列。请验证您的备份。

# 监控

进步源于一种名为 `PROMON` 的优秀字符模式数据库监控器。DBA 应该熟悉 `PROMON` 的交互模式，并习惯其系统的正常值范围。但监控的真正威力是通过对长时间的活动持续收集历史视图获得的。然后您可以使用它以更具针对性且更可靠的方式验证有关某个问题的假设。以下脚本可以作为收集此类数据的基础：

# 监控
#

```
. /mnt/scripts/env    # export TMP=/mnt/tmp

TM=`date "%H.%M"`

DLC/bin/promon $DBNAME > $LOGS/sample.$TM << "EOF" 2 > /dev/null

```

R&D
5
3
300
1
9999
P
2
1
s
p
xEOF

```

此脚本启动了 **PROMON**，进入 R&D 菜单（比默认菜单更详细），并将采样间隔调整为 300 秒，每页输出行数调整为 9999。它备份一个菜单并进入活动摘要屏幕，收集自数据库启动以来的摘要以及五分钟期间的活动样本，然后退出。

01/18/00 活动：摘要

15:04:35 14:59 to 01/18/00 15:04 (5 min 1 sec)

| 事件 | 总计 | 每秒 | 事件 | 总计 | 每秒 |

|---|---|---|---|---|---|

| 提交 (Commits) | 17951 | 59.6 | 数据库读取 (DB Reads) | 26059 | 86.5 |

| 回滚 (Undos) | 2 | 0.0 | 数据库写入 (DB Writes) | 903 | 3.0 |

| 记录读取 (Record Reads) | 1219453 | 4051.3 | BI 读取 (BI Reads) | 0 | 0.0 |
