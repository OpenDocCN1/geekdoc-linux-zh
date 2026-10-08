

# 高级 Bash 脚本指南

```bash
trap -rm $TEMPFILE; exit $USER_INTERRUPT TERM INT
# 如果脚本被控制-C 中断，则清理临时文件。
```

```bash
echo

while [ $TRUE ]; # 无限循环。
do
    tail -n $CHECK_LINES $LOGFILE > $TEMPFILE
    # 将系统日志的最后 100 行保存为临时文件。
    # 这是有必要的，因为较新的内核在启动时会产生大量日志。
    search=$(grep $KEYWORD '$TEMPFILE')
    # 检查是否存在 "IP address" 字符串，
    # 表示登录成功。

    if [ -z "$search" ]; # 因为可能存在空格，所以必须加引号。
    then
        echo "On-line"
        rm -f $TEMPFILE # 清理临时文件。
        exit $ONLINE
    else
        echo -n "." # echo -n 选项抑制换行，
        # 这样你就能看到连续的点点。
    fi
    sleep 1
done
```

# 注意：如果你将 KEYWORD 变量更改为 "Exit"，
# 此脚本可以在在线状态下使用，
# 用于检查意外的注销。

# 练习：根据上面的注释修改脚本，
# 并对其进行美化。

exit 0

# Nick Drags 提供了另一种方法

```bash
while true
do
    if doconfig ppp0 | grep UP 1 >/dev/null && echo "connected" && exit 0
    echo -n "." # 在连接上之前打印点（....）。
    sleep 2
done
```

# 问题：通过按下 Control-C 终止此进程可能是不够的。
# （点点可能会持续输出）。
# 练习：修复这个问题。

# Stephane Chazelas 还有另一种替代方案：

```bash
CHECK_INTERVAL=1

while tail -n 1 "$LOGFILE" | grep -q "$KEYWORD"
do
    echo -n.
    sleep $CHECK_INTERVAL
done
echo "On-line"
```

## 第 32 章 调试

# 练习：讨论这些各种方法的各自相对优缺点。

### 示例 32-7。进度条的简单实现

```bash
# /bin/bash
# progress-bar2.sh
# 作者: Graham Ewart（由 ABS Guide 作者重新格式化）。
# 经许可在 ABS Guide 中使用（感谢！）。

 使用 bash 运行此脚本。它对 sh 不有效。

interval=1
long_interval=10
{
  trap "exit" SIGUSR1
  sleep $interval; sleep $interval
  while true
  do
    echo -n '.' # 使用点。
    sleep $interval
  done) & # 将进度条作为后台进程启动。
}
```

```bash
pid=$!
trap "echo 'long-running process ' kill -USR $pid; wait $pid" EXIT # 用于处理 ^C。

echo -n 'long-running process ' 
sleep $long_interval
echo ' Finished!'

kill -USR $pid
wait $pid # 停止进度条。
trap EXIT

exit $?
```

trap 的 DEBUG 参数会导致脚本中的每条命令执行后执行指定的操作。它允许对变量进行追踪等。

### 示例 32-8。追踪变量

```bash
# /bin/bash
trap 'VARIABLE-TRACE\ $variable = \"$variable\"' DEBUG
# 在每条命令后回显 $variable 的值。

variable=29; line=$LINENO

echo " Initialized $variable to $variable in line number $line."

let "variable *= 3"; line=$LINENO
echo " Just multiplied $variable by 3 in line number $line." # 注意：此处原文 echo 漏掉了变量

exit 0
```

```bash
# "trap command1 . . command2 . . 'DEBUG'" 结构
# 在复杂脚本的上下文中更合适，
```

## 第 32 章 调试

当然，trap 在调试之后还有其他用途，例如在脚本内部禁用按键输入（示例 A-43）。

### 示例 32-9。运行多个进程（在 SMP 机器上）

```bash
#!/bin/bash
# parent.sh
# 在 SMP 机器上运行多个进程
# 作者: Tedman Eng

# 这是两个脚本中的第一个，
# 两个都必须存在于当前目录。

LIMIT=$1                # 要启动的进程总数
NUMPROC=4              # 并发线程数（fork）
PROCID=1               # 起始 ID
echo "My PID is $$"

function start_thread() {
  if [ $PROCID -le $LIMIT ]; then
    ./child.sh $PROCID
  else
    echo "Limit reached."
    wait
  fi
}

while [ $NUMPROC -gt 0 ]; do
  start_thread;
  let "$NUMPROC--"
done

while true
do
  trap "start_thread" SIGTERM
done
```

（注：此处原文后续似乎出现了乱码或重复，已根据逻辑翻译剩余部分）

# 原文逻辑：# 这是两个脚本中的第一个，
# 两个都必须存在于当前目录。

LIMIT=$1                # 要启动的进程总数
NUMPROC=4              # 并发线程数（forks）
PROCID=1               # 起始 ID
echo "My PID is $$"

function start_thread() {
  if [ $PROCID -le $LIMIT ]; then
    ./child.sh $PROCID
  else
    echo "Limit reached."
    wait
  fi
}

while [ $NUMPROC -gt 0 ]; do
  start_thread;
  let "$NUMPROC--"
done

while true
do
  trap "start_thread" SIGTERM
done
```

（注：由于提供的原文文本从此处开始出现了大量重复和无意义的字符，如 "Nick Drags an alternate method" 之后的内容逻辑混乱，作为高级文档工程师，我已尽可能翻译了可理解的结构化部分。针对原文中的乱码部分，保持了格式。）

