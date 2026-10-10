
`procopy empty /mnt/db/mydata`

空数据库是 `procopy` 命令的一个特例。尽管它存在于安装 Progress 可执行文件的 DLC 目录中，但没有必要指定该结构的完整路径。Progress 将使用 DLC 环境变量找到空数据库。还有几个基于块大小的空数据多个版本。要创建一个使用 8k 块大小的数据库，只需在 `procopy` 命令中将 `empty` 替换为 `8k` 即可。但请记住，可变块大小是企业版数据库的功能。现在数据库已准备好单用户模式访问。为了允许超过一个用户，必须启动多用户代理（broker）。在没有其他选项的情况下，代理将允许本地系统的 10 个用户。要允许更多用户，请使用 `-N` 选项。这些选项以及更多与性能相关的参数将在后文中以及《系统管理参考》中进行讨论。

## 调整缓冲区池的大小

在大多数安装中，内存最大的使用者是缓冲区池（buffer pool）。这是一个大型共享区域，用于缓存磁盘块以提高性能。不要按用户进行调优！要根据磁盘 I/O 能处理的能力进行调优，直到你的磁盘利用率在 50% 左右，没有队列且服务时间在 20ms 以下。如果你的磁盘平均访问时间为 10ms，那么它们每秒可以执行 100 次随机 I/O 操作，并在无队列的情况下维持每秒 25 到 50 次 I/O 操作。用户数量与请求数量有关，缺失率是非线性的。它遵循类似的曲线：

`R = L / sqrt(C)`

其中：
- `R` = 物理 I/O 操作
- `L` = I/O 操作
- `B` = 缓冲区池大小
- `C` = 接近 1.5 的常数

因此，这里没有可以适用的每用户内存量规则。虽然在大致范围内，但每个用户 2MB 通常是一个很好的猜测。一旦你有了数据，就可以精确调整该值以更好地满足目标 I/O。图 8.7 提供了一个示例。

### 图 8.7 使用示例数据满足目标 I/O

| 逻辑读取 | B | I/O 操作数 | 命中率 | 缺失率 |
|---|---|---|---|---|
| 1,000,000 | 5,000 | 11,547 | 98.845% | 1.155 |
| 1,000,000 | 10,000 | 8,165 | 99.184% | 0.816 |
| 1,000,000 | 15,000 | 6,667 | 99.333% | 0.667 |
| 1,000,000 | 20,000 | 5,774 | 99.423% | 0.577 |
| 1,000,000 | 25,000 | 5,164 | 99.484% | 0.516 |
| 1,000,000 | 30,000 | 4,714 | 99.529% | 0.471 |
| 1,000,000 | 35,000 | 4,364 | 99.564% | 0.436 |
| 1,000,000 | 40,000 | 4,082 | 99.592% | 0.408 |
| 1,000,000 | 45,000 | 3,849 | 99.615% | 0.385 |
| 1,000,000 | 50,000 | 3,651 | 99.635% | 0.365 |
| 1,000,000 | 55,000 | 3,482 | 99.652% | 0.348 |
| 1,000,000 | 65,000 | 3,203 | 99.680% | 0.320 |
| 1,000,000 | 70,000 | 3,086 | 99.691% | 0.309 |
| 1,000,000 | 75,000 | 2,981 | 99.702% | 0.298 |
| 1,000,000 | 80,000 | 2,887 | 99.711% | 0.289 |

## 运行进度

Progress 数据库的典型日常运行通常不是一项全职工作。通常会为数据库的启动、备份和关闭编写一些初始脚本。之后，大部分时间都花在收集数据上，以确保系统的最佳性能。许多基于 Progress 的系统可以运行多年，而无需数据库管理员（DBA）的关注。

## 管理数据库

PSC 提供了用于启动、停止、监控和备份数据库的简单脚本。虽然这些脚本对于初始开发环境通常足够了，但生产工作通常需要更复杂或更定制化的方法。

一个有帮助的第一步是创建一个小型的环境脚本，将所有常用的 Progress 和与应用程序相关的环境变量包含在一个脚本中，然后在需要的脚本中对其进行“点源（dotted）”或“加载（sourced）”。例如：

```bash
## Common Environment Script

### 使用方法:

### . /mnt/scripts/env

export TMP=/mnt/tmp

export MTH=$(date '+%m)

export DAY=$(date '+%d)

export LOGS=/mnt/logs/$MTH.$DAY

export SRV=$(uname)

export SCRIPTS=/mnt/scripts

export DLC=/opt/progress/dlc83b

export DBNAME=/mnt/db/sports
```

```bash
### 标准消息处理程序

msg()
{
  MSG=$1; shift
  echo "MSG"
  echo 'date' "$MSG" >> $LOGS/start.log
  # 如果传递了额外的参数，则将消息发送给
  # 这些人员（名称可能是分页器地址）
  if [ "$1" != "" ]; then
    echo SRV: $(date) "$MSG" | mailx -s "$MSG" "$@"
  fi
}
```

### 启动

较小的站点通常使用脚本来自动检测数据库状态，并在第一个用户尝试访问时将其启动。有时它们会在最后一个用户退出时自动将其关闭。尽管这样做很方便，但这种方法有几个潜在的陷阱。此类脚本绝不应删除 `.lk` 文件。如果 Progress 提示存在锁文件，你需要认真对待此信息并理解它为什么会在那里。可能是因为另一个用户在在你不知情的情况下启动了合法的单用户会话（可能是为了进行数据库维护）。删除 `.lk` 文件后访问数据库将导致两组进程，它们可能在互不知情的情况下同时更新数据库——这种情况显然会导致灾难。

这种方法的另一个缺点是，它很难为维护或恢复窗口获得对数据库的独占访问。良好的做法是将数据库服务器的启动与用户会话的启动分开，并建立一套所有脚本都遵守的标准控制措施，以便在需要时安全地管理数据库。一种非常有用的技术是使用标志位来限制用户会话的访问，如下所示：

```bash
### Start server
#
/mnt/scripts/env
```

```bash
### 启动某些内容并验证
str()
{
  CMD=$1
  USR=$2
  GTX=$3
  WHO=$4
  msg "Starting: $1"
  $CMD >> $LOGS/start.log
  sleep 5
  ps -fu $USR | grep "GTX" > /dev/null
  if [ $? = "1" ]; then
    msg "**** $CMD did not start" $WHO
    exit 0
  else
    msg "++++ $CMD started successfully"
  fi
}
```

```bash
### Create logging directory
if [ ! -d $LOGS ]; then
    mkdir $LOGS
    chmod 755 $LOGS
fi
```

```bash
msg "Starting database"
msg "Locking out users"
echo "Starting Database - Please wait" > $TMP/User_Lockout
chmod 644 $TMP/User_Lockout
rm -f $TMP/DB_IS_UP
sleep 5
```

```bash
$DLC/bin/_mprosrv -pf $SCRIPTS/db.pf \
progress \
    "[m]prosrv" \
dba
```

```bash
$DLC/bin/_mprshut $DBNAME -C biw \
progress \
    "[b]iw" \
dba
```

```bash
$DLC/bin/_mprshut $DBNAME -C aiw \
progress \
    "[a]iw" \
dba
```

```bash
$DLC/bin/_mprshut $DBNAME -C apw \
progress \
    "[a]pw" \
dba
```

```bash
dba
$DLC/bin/mprshut $DBNAME -C watchdog \
progress \
"[w]atchdog" \
dba
```

```bash
msg "Creating DB_IS_UP file..."
```
