
- 捕获信号并执行特定于信号的命令。此方法要求程序定义一个在接收到信号时执行的函数。这是处理信号最复杂且最强大的方法。

第一种方法是所有 shell 脚本的默认行为。迄今为止您查看过的所有脚本都使用此方法处理信号。本节说明使用第二种和第三种方法的脚本。

## trap 命令

trap 命令设置和取消在接收到信号时采取的操作。其语法是

```
trap name sigs
```

这里 name 要么是一组命令的列表，要么是要执行的 shell 函数的名称，而 sigs 是一组信号的列表。当脚本接收到 sigs 中列出的信号时，name 指定的命令将被执行。如果省略 name，trap 会将给定 sigs 的操作重置为默认操作。

trap 的一些常见用途是

- 清理临时文件
- 始终忽略信号
- 仅在关键操作期间忽略信号

我们将在本章后面介绍第四种用途，即设置计时器。

## 清理临时文件

如果脚本创建了临时文件，通常的做法是在脚本退出前删除这些文件。大多数脚本在正常执行期间能正确执行此类清理，但很少有脚本在信号发生时执行适当的清理操作。请考虑以下脚本：

```
#!/bin/sh
TMPF=.arch
uname -m > $TMPF
read ARCH < $TMPF
rm -f $TMPF
echo $ARCH
exit 0
```

此脚本创建了一个临时文件 .arch，并在退出前将其删除。在正常情况下，脚本退出后临时文件将不存在。然而，

如果接收到信号，临时文件可能不会被删除。为了解决这个问题，我们可以使用 trap 如下：

```
trap 'rm -f $TMPF; exit 2' 1 2 3 15
```

当接收到 SIGHUP、SIGINT、SIGQUIT 或 SIGTERM 信号时，临时文件将被删除，并以返回代码 2 调用 exit，表示脚本在异常情况下退出。通常脚本正常退出时，其退出代码为 0。如果发生任何异常，退出代码应为非零。

有时需要更复杂的清理。在这种情况下，应使用 shell 函数或信号处理程序。例如，我们可以修改 uu 脚本（在第 13 章“参数”中描述）使其具备信号安全性，可以添加类似以下内容：

```
cleanup() {
  if [ -f "$OUTFILE" ] ; then
    print "Cleaning Up...";
    rm -f "$OUTFILE" 2> /dev/null ;
    echo "Done."
  fi
}
trap cleanup 1 2 3 15
```

函数 Cleanup 将在脚本接收到 SIGHUP、SIGINT、SIGQUIT 或 SIGTERM 信号时被调用。此函数会删除脚本的输出文件（如果该文件存在）。通过在接收到信号时进行清理，不会留下部分编码的文件来混淆用户。

## 多个信号处理程序

在前面的示例中，单个信号处理程序用于所有信号。这不是严格要求，并且经常不同信号有不同的处理程序。例如，以下 trap 命令完全有效：

```
trap cleanup 2 15
trap init 1
```

```
echo "Usage: $0 cmd."
exit 1
fi

Init() {
  if [ "$1" != "" -a "$1" != "0" ] ; then
    if kill -0 $1 > /dev/null 2>&1 ; then
      kill $1 > /dev/null 2>&1 || return
    fi
  fi
  $PROG &
}

Cleanup() {
  if [ "$1" != "" -a "$1" != "0" ] ; then
    kill -9 $1 > /dev/null 2>&1
  fi
  exit 2
}

trap Cleanup 2 3 15
trap Init 1

while ; ;
do
  if [ "$1" != "" -a "$1" != "0" ] ; then
    wait $1
  fi
  $PROG &
done

exit 0
```

此脚本在后台启动作为第一个参数指定的程序，并等待该程序终止。如果程序终止，它将被再次启动。脚本在接收到 SIGINT、SIGQUIT 或 SIGTERM 时退出。如果脚本接收到 SIGHUP，它会尝试重新启动程序。

## 忽略信号

在某些情况下，如果接收到信号，很难进行清理。在这种情况下，忽略信号比处理它们更好。忽略信号有两种方法：

```
trap '' sigs
trap : sigs
```

这里，sigs 是要忽略的信号列表。第一种形式向 trap 传递一个空 ('') 参数，trap 将其解释为忽略。第二种形式指定要执行的命令

为 :，这是一个空操作命令，如你可能回忆的那样。由于两种形式产生相同的结果，请随意使用其中任何一种。

作为示例，我们可以通过在脚本开头添加以下行来更新第 12 章中的 uu 脚本以忽略所有信号：

```
trap '' 1 2 3 15
```

## 在关键操作期间忽略信号

如果你在脚本开头指定如下的 trap 命令

```
trap '' 1 2 3 15
```

脚本将忽略所有信号直到完成。从程序员的角度来看，这似乎是个好主意，但从用户的角度来看则不是。理想的方法是仅在脚本的最关键部分期间忽略信号。这允许用户终止脚本，同时确保关键操作不会被信号中断而执行。

假设我们有一个 shell 脚本，其中有一个名为 DoImportantStuff() 的 shell 函数，不应被信号中断。为了确保此函数不被中断，你可以在调用函数之前安装信号处理程序，并在调用完成后将其重置：

```bash
trap '' 1 2 3 15
DoImportantStuff
trap 1 2 3 15
```

第二次调用 trap 只有信号参数。这会导致 trap 将每个信号的处理程序重置为默认处理程序。

## 设置计时器

在许多脚本中，存在执行需要大量时间完成的命令的关键部分。在极少数情况下，这些命令可能无法完成处理。为了解决这种情况，你需要在脚本中设置一个计时器。当计时器到期时，脚本应终止并通知用户问题。在本节中，你将查看一个简单的脚本，演示使用 SIGALARM 结合信号处理程序设置计时器的主要方面。

我们脚本的主体执行以下操作：

- 1. 为 SIGALARM 设置处理程序。
- 2. 设置计时器。
- 3. 执行程序。
- 4. 等待程序执行完成。
- 5. 取消设置计时器。

如果计时器在程序执行完成前到期，SIGALARM 的处理程序应终止程序。

主体类似于以下内容：

```bash
# main()
trap AlarmHandler 14
SetTimer 15
SPROG &
CHPROGIDS="$CHPROGIDS $!"
wait $!
UnsetTimer
echo "All Done."
exit 0
```

主体中唯一之前未提及的是 CHPROGIDS 变量。此变量维护脚本启动的进程的 PID 列表，以便 SIGALARM 的信号处理程序可以终止这些进程。

### AlarmHandler

现在让我们来看一下 SIGALARM 的信号处理程序 AlarmHandler：

```bash
AlarmHandler() {
  echo "Got SIGALARM, cmd took too long."
  KillSubProcs
  exit 14
}
```

这是一个简单的函数，它向屏幕打印一条消息，调用函数 KillSubProcs，并以退出代码 14 退出。此退出代码用于指示警报被触发。

KillSubProcs 函数杀死脚本的所有子进程，这些进程存储在变量 CHPROGIDS 中：

```bash
KillSubProcs() {
  kill ${CHPROGIDS:-$!}
  if [ $? -eq 0 ]; then
    echo "Sub-processes killed."
  fi
}
```

这是一个简单的函数，它向屏幕打印一条消息，调用函数 KillSubProcs，并以退出代码 14 退出。此退出代码用于指示警报被触发。

KillSubProcs 函数杀死脚本的所有子进程，这些进程存储在变量 CHPROCSIDS 中：

```
KillSubProcs() {
  kill $CHPROCSIDS
  if [ $? -eq 0 ] ; then
    echo "Sub-processes killed."
  fi
}
```

### SetTimer

一旦 SIGALARM 的信号处理程序就位，我们需要一个设置计时器的函数。我们使用的函数是 SetTimer：

```
SetTimer() {
  DEF_TOUT=${1:-10}
  if [ $DEF_TOUT -ne 0 ] ; then
    sleep $DEF_TOUT & kill -s 14 $$
    CHPROCSIDS="$CHPROCSIDS $!"
    TIMERPROC=$!
  fi
}
```

此函数接受一个参数，表示计时器应设置的秒数。默认值为 10 秒。

计时器本身相当简单；它只是命令
sleep $DEF_TOUT & kill -s 14 $$
在后台执行。此命令使用 sleep 等待一段时间（存储在 $DEF_TOUT 中），之后使用 kill 向脚本发送 SIGALRM（请记住脚本的 PID 存储在 $$ 中）。

由于计时器在后台运行，我们需要使用其 PID 更新子进程列表 $CHPROCSIDS。我们还将计时器的 PID 保存到 $TIMERPROC，以便以后在需要取消设置计时器时使用它。

### UnsetTimer

最后，我们需要一个函数来取消 SetTimer 启动的计时器。UnsetTimer 函数通过使用 kill 终止计时器来实现这一点（SetTimer 将计时器的 PID 保存到 $TIMERPROC 中）：

```
UnsetTimer() {
  kill $TIMERPROC
}
```
