
```bash
echo "成功: 预事件脚本完成 RC - $RC" >> $LOGFILE
else
    echo "失败: 预事件脚本失败 RC - $RC" > $TTY
    echo "失败: 预事件脚本失败 RC - $RC" >> $LOGFILE
fi

echo "等待 $PROCESS ..."
integer PROC_COUNT='1' # 初始化

# 循环直到至少有一个进程运行
until (( "$PROC_COUNT" > 0 ));
do
    # 这是一个协进程。它检查是否发生了
    # “程序中断”。如果是，`BREAK` 将为
    # 'Y'，我们退出循环和函数。
    read BREAK

    if [[ $BREAK = 'Y' ]];
    then
        return 3
    fi

    PROC_COUNT=$(ps aux | grep -v "grep $PROCESS" | \
        grep -v $SCRIPT_NAME | \
        grep $PROCESS | wc -l) >/dev/null 2>&1

    sleep $INTERVAL # 需要降低 CPU 负载！
done

RUN='Y' # 开启运行
TIMESTAMP=$(date +%D%T)
PID_LIST=$(ps aux | grep -v "grep $PROCESS" | \
    grep -v $SCRIPT_NAME | \
    grep $PROCESS | awk '{print $2}')

if (( "$PROC_COUNT" -eq 1 ));
then
    echo "启动进程: $PROCESS 开始时间 ===" >> $TIMESTAMP
    echo "活跃 PID: $PID_LIST" >> $LOGFILE
    echo "启动进程: $PROCESS 开始时间 ===" > $TTY
    echo "活跃 PID: $PID_LIST" > $TTY
elif (( "$PROC_COUNT" -gt 1 ));
then
    echo "启动进程: $PROC_COUNT 开始时间 ==$TIMESTAMP" >> $LOGFILE
    echo "活跃 PID: $PID_LIST" >> $LOGFILE &
    echo "启动进程: $PROC_COUNT 开始时间 ==$TIMESTAMP" > $TTY
    echo "活跃 PID: $PID_LIST" > $TTY
fi
done
```

####################
## 主程序开始
####################

### 设置 TRAP

```bash
trap 'BREAK='\''Y'\'';print $BREAK 2>/dev/null;trap_exit'
```

```bash
BREAK='N' # BREAK 变量用于协进程 proc_watch
PROCESS= # 初始化
integer TOTAL_SECONDS=0

# 检查命令行参数
if (( $# > 10 || $# < 2 ));
then
    usage
    exit 1
fi

# 检查是否只有秒和进程名作为参数
if [[ ($# -eq 2) && ($1 != *) && ($2 != *) ]];
then
    NUM_TEST=$(test_string $1) # 是整数吗？
    if [[ "$NUM_TEST" = 'POS_INT' ]];
        PROCESS=$2 # 是，这是一个整数
    fi          # 可以是任意内容
else
    usage
    exit 1
fi

# 由于 getopts 不关心获取什么参数，
# 我们进行快速合法检查，确保只有
# 2 到 10 个参数，且第一个必须以 -*（连字符和任意内容）开头，否则报错。
case "$#" in
    [2-10]) [[ $1 != * ]]; then
        usage; exit 1
    fi
    ;;
esac
exit 0

HOURS=0 # 全部初始化零
MINUTES=0
SECS=0
DAYS=0
```

```bash
# 对于天、小时、分钟和天的每个 OPTARG，
# 使用 check_string 函数检查其是否为整数
while getopts "h:H:M:s:D:D:P" OPT_LIST 2>/dev/null
do
    case $OPT_LIST in
        h|H) [[ $(test_string $OPTARG) != 'POS_INT' ]] && usage && exit 1
            (( HOURS = $OPTARG * 3600 )) # 每小时3600秒
            ;;
        m|M) [[ $(test_string $OPTARG) != 'POS_INT' ]] && usage && exit 1
            (( MINUTES = $OPTARG * 60 )) # 每分钟60秒
            ;;
        s|S) [[ $(test_string $OPTARG) != 'POS_INT' ]] && usage && exit 1
            SECS="$OPTARG" # 秒就是秒
            ;;
        d|D) [[ $(test_string $OPTARG) != 'POS_INT' ]] && usage && exit 1
            (( DAYS = $OPTARG * 86400 )) # 每天86400秒
            ;;
        p|P) PROCESS=$OPTARG # 进程可以是任意内容
            ;;
        \? ) usage # 用法错误
            exit 1
            ;;
        :) usage # 用法错误
            exit 1
            ;;
        \*) usage # 用法错误
            exit 1
            ;;
    esac
done
```

```bash
if [[ $SECS -gt 0 || $MINUTES -gt 0 || $HOURS -gt 0 \
    || $DAYS -gt 0 ]]
then
    (( TOTAL_SECONDS = SECS + MINUTES + HOURS + DAYS ))
fi
```

# 最后最后的检查！

```bash
if (( TOTAL_SECONDS <= 0 )) || [ -z $PROCESS ]
then
    # 要不是没有需要计数的秒，
    # $PROCESS 变量为空...用法...
    usage
    exit 1
fi
```

################ 在此处开始监控 #################

```bash
echo "currently running $PROCESS processes:\n" > $TTY
ps aux | grep -v "$PROCESS" | grep -v $SCRIPT_NAME \
    grep $PROCESS > $TTY
```

`PROC_RC=$?` 获取被监控函数的初始状态

```bash
echo ->$TTY 向屏幕发送空行
(( PROC_RC != 0 )) && echo "\此处没有运行 $PROCESS 进程\n"
if (( PROC_RC == 0 )) && echo "目标进程正在运行..."
then
    RUN='Y' # 将 RUN 标志置为 true 或 yes。
    integer PROC_COUNT=$(ps aux | grep -v "$PROCESS" | grep -v \
        $SCRIPT_NAME | grep $PROCESS | wc -l) >/dev/null 2>&1
    if (( PROC_COUNT == 1 ))
    then
        echo "$PROCESS 进程当前正在运行\n......\n"
    elif (( PROC_COUNT > 1 ))
    then
        print "当前有 $PROC_COUNT 个 $PROCESS 进程正在运行...监控中...\n"
    fi
else
```

```bash
echo "$PROCESS 进程当前未运行...监控中..."
RUN='N' # 将 RUN 标志置为 false 或 no。
fi

TIMESTAMP=$(date +%D%T) # 此脚本开始监控的时间

# 获取当前活跃的进程 ID 列表
```
