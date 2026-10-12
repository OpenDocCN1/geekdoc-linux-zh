
# 第10章 进程监控与预处理

## 列表 10-8 使用协进程的示例

在列表 10-8 的代码块中，我们定义了 `proc_watch` 函数，这是我们想要作为后台进程启动的函数。如你所示，`proc_watch` 函数有一个无限循环。如果主脚本被中断，那么如果没有退出 `proc_watch` 后台函数中循环的方法，该循环将继续执行！为了解决这个问题，我们使用管道符号 `&` 作为后缀，通过“将其管道到后台”将 `proc_watch` 作为协进程启动。当我们想从主脚本与函数通信时，我们使用标准的 `read` 命令 `BREAK_OUT`。协进程是我们将在主脚本因捕获到信号（trapped signal）被中断时跳出循环的机制，并确保在脚本结束时不会终止命令。当然，我们永远无法通过 `trap` 捕获 `-9`。使用 `trap` 捕获信号，在脚本结束时不会终止。由于我们预计可能会输入错误的命令行参数，我们可以直接忽略这些消息并通过重定向到 `/dev/null`（即位桶）将它们丢弃。

```bash
# 注释掉上面的冒号，':'

STARTUP_RC=$$

return $$STARTUP_RC

}

############################################################

post_event_script ()

{

# 将你希望在监控进程结束后 
# 执行的任何内容放在此函数中

  : 无操作 - 需要作为空函数的占位符

# 注释掉上面的冒号，':'

POST_RC=$$

return $POST_RC

}

############################################################

# 此函数用于测试字符字符串

test_string ()

{

if (( $# != 1 ));

then

    echo 'ERROR'

    return

fi

C_STRING=$1

# 测试字符字符串的组成

case $C_STRING in

    +([0-9]) echo 'POS_INT' # 整数 >= 0

    ;;

    +(-0-9]) echo 'NEG_INT' # 整数 < 0

    ;;

    +([a-z]) echo 'LOW_CASE' # 小写文本

    ;;

    +([A-Z]) echo 'UP_CASE' # 大写文本

    ;;

    +([a-z]|[A-Z]) echo 'MIX_CASE' # 混合大小写文本

    ;;

    *) echo 'UNKNOWN' # 其他任何

esac

}

############################################################

proc_watch ()
```

## Listing 10-9 (续)

```bash
{

# set -x # 取消注释以调试此函数

# 此函数负责所有的进程监控！

while :;

  # 无限循环！！

  case $RUN in

    'Y')

      # 这将运行 startup_event_script，这是一个函数

      if [[ $RUN_STARTUP_EVENT = 'Y' ]]

      then

        echo "启动事件: 正在执行启动事件脚本..."

        >> $TTY

        echo "启动事件: 正在执行启动事件脚本..."

        >> $LOGFILE

        startup_event_script # 用户定义函数!!!

        RC=$? # 检查返回码!!

        if (( "$RC" == 0 ));

        then

          echo "成功: 启动事件完成 RC - $RC" > $TTY

          echo "成功: 启动事件完成 RC - $RC" >> $LOGFILE

        else

          echo "失败: 启动事件脚本失败 RC - $RC" > $TTY

          echo "失败: 启动事件脚本失败 RC - $RC" >> $LOGFILE

        fi

      fi

      integer PROC_COUNT='-1' # 重置计数器

      integer LAST_COUNT='-1'

      # 循环持续直到进程结束

      until (( "$PROC_COUNT" == 0 ));

      do

        # 此函数是一个协进程 (Co-Process)。$BREAK 用于检查
        # 是否发生了“程序中断”。如果是，BREAK 将为
        # 'Y'，我们将同时退出循环和函数。

        read BREAK

        if [[ $BREAK = 'Y' ]]

        then

          return 3

        fi

}
```

## Listing 10-9 (续)

```bash
PROC_COUNT=$(ps aux | grep -v "grep $PROCESS" | \
  grep -v $SCRIPT_NAME | \
  grep $PROCESS | wc -l) >/dev/null 2>&1

if [ "$LAST_COUNT" -gt 0 && "$LAST_COUNT" != "$PROC_COUNT" ];

then

  # 进程数量发生了变化...

  TIMESTAMP=$(date +%D%T)

  # 获取所有进程的 PID 列表

  PID_LIST=$(ps aux | grep -v "grep $PROCESS" | \
  grep -v $SCRIPT_NAME | \
  grep $PROCESS | awk '{print $2}')

  echo "进程数量: $PROC_COUNT" >> $LOGFILE

  echo "正在运行的进程 ==$TIMESTAMP" >> $LOGFILE

  echo "进程数量: $PROC_COUNT" >> $LOGFILE

  echo "正在运行的进程 ==$TIMESTAMP" > $TTY

  echo "活跃 PID: $PID_LIST" >> $LOGFILE &

  echo "活跃 PID: $PID_LIST" > $TTY

fi

  LAST_COUNT=$PROC_COUNT

  sleep $INTERVAL # 需要降低 CPU 负载！

done

RUN='#' # 关闭 RUN 标记

TIMESTAMP=$(date +%D%T)

echo "结束进程: $PROCESS 结束时间 ===" \
echo "$TIMESTAMP" >> $LOGFILE

echo "结束进程: $PROCESS 结束时间 ===" \
echo "$TIMESTAMP" > $TTY

  # 这将运行 post_event_script，这是一个函数

if [[ "$PROC_EVENT" = 'Y' ]];

then

  echo "后事件: 正在执行后事件脚本..." \
  > $TTY

  echo "后事件: 正在执行后事件脚本..." \
  >> $LOGFILE &

  post_event_script # 用户定义函数!!!

  integer RC=$?

  if [ "$RC" == 0 ];

  then

    echo "成功: 后事件脚本完成 RC - $RC" > $TTY
```

## Listing 10-9 (续)

```bash
echo "成功: 后事件脚本完成 RC - $RC" >> $LOGFILE

else

    echo "失败: 后事件脚本失败 RC - $RC" > $TTY

    echo "失败: 后事件脚本失败 RC - $RC" >> $LOGFILE

fi

RUN='N'

# 这将运行 pre_event_script，这是一个函数

if [[ $RUN_PRE_EVENT == 'Y' ]];

then

    echo "预事件: 正在执行事件脚本..." > $TTY

    echo "预事件: 正在执行事件脚本..." >> $LOGFILE

  pre_event_script # 用户定义函数!!

  RC=$?

  if (( "$RC" -eq 0 ));

  then

    echo "成功: 预事件脚本完成 RC - $RC" > $TTY
```
