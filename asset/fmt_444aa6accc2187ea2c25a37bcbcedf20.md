
# 说明

- 1 显示了 `myfunctions` 文件。它包含两个函数定义。
- 2 定义的第一个函数名为 `go`。它将主提示符设置为当前工作目录。
- 3 定义的第二个函数名为 `greetings`。它会向作为参数传入的用户名致意。
- 4 `source` 或点命令将 `myfunctions` 文件的内容加载到 shell 的内存中。现在，这两个函数都已为此 shell 定义。
- 5 调用并执行 `greetings` 函数。

## 示例 14.60

（下面显示的 `dbfunctions` 文件包含供主程序使用的函数。完整脚本参见 `cd`。）

```
1 $ cat dbfunctions

2 function addon () {    # Function defined in file dbfunctions

3   while true
    do
      echo "Adding information "
      echo "Type the full name of employee "
      read name
      echo "Type address for employee "
      read address
      echo "Type start date for employee (4/18/88) :"
      read startdate
      echo $name:$address:$startdate
      echo -n "Is this correct? "
      read ans
      case "$ans" in
        [Yy]*)
          echo "Adding info..."
          echo $name:$address:$startdate>>datafile
          sort -u datafile -o datafile
          echo -n "Do you want to go back to the main menu? "
          read ans
          if [[ $ans == [Yy] ]]
          then
4           return    # Return to calling program
          else
```

## 示例 14.60（续）

```
5    continue  # Go to the top of the loop
    fi
    ;;
)
 echo "Do you want to try again? "
 read answer
 case "$answer" in
   [Yy]*) continue;;
   *) exit;;
 esac
    ;;
 done
 esac
6 }    # End of function definition
```

（命令行）
```
7 $ more mainprog
#!/bin/bash
# Scriptname: mainprog
# This is the main script that will call the function, addon

datafile=$HOME/bourne/datafile
8 source dbfunctions   # The file is loaded into memory
 if [ ! -e $datafile ]
 then
   echo "$ (basename $datafile) does not exist" >&2
   exit 1
 fi
9 echo "Select one: "
 cat <<EOF
 [1] Add info
 [2] Delete info
 [3] Update info
 [4] Exit
 EOF
 read choice
 case $choice in
10 1) addon        # Calling the addon function
    ;;
    2) delete      # Calling the delete function
    ;;
    3) update
    ;;
```

## 示例 14.60（续）

```
4)
    echo Bye
    exit 0
    ;;
5) echo Bad choice
    exit 2
    ;;
esac
echo Returned from function call
echo The name is $name
# Variable set in the function are known in this shell.
done
```

# 说明

- 1 显示了 `dbfunctions` 文件。
- 2 定义了 `addon` 函数。它的作用是向 `datafile` 添加新信息。
- 3 进入 `while` 循环。除非在循环体中包含 `break` 或 `continue` 等循环控制语句，否则它将永远循环下去。
- 4 `return` 命令将控制权返回到调用函数的调用程序。
- 5 控制权返回到 `while` 循环的顶部。
- 6 右花括号结束函数定义。
- 7 这是主脚本。此脚本将使用 `addon` 函数。
- 8 `source` 命令将 `dbfunctions` 文件加载到程序的内存中。现在，`addon` 函数已为此脚本定义，可供使用。就好像你刚刚在脚本中的这个位置定义了该函数一样。
- 9 使用 here 文档显示菜单。要求用户选择一个菜单项。
- 10 调用 `addon` 函数。

### 14.8 捕获信号

当你的程序正在运行时，如果你按下 `Ctrl-C` 或 `Ctrl-\`，一旦信号到达，你的程序就会立即终止。有时你可能不希望程序在信号到达后立即终止。你可以安排忽略该信号并继续运行，或在真正退出脚本之前执行某种清理操作。`trap` 命令允许你控制程序在接收信号时的行为。

信号被定义为一种异步消息，它由一个数字组成，该数字可以从一个进程发送到另一个进程，或者当某些键被按下时由操作系统发送给进程。

被按下，或者发生了某些异常情况时。⁶ `trap` 命令告诉 shell 在接收到信号时终止当前正在执行的命令。如果 `trap` 命令后面跟有引号内的命令，则当收到指定信号时，将执行该命令字符串。shell 会读取命令字符串两次：一次是在设置 `trap` 时，另一次是在信号到达时。如果命令字符串被双引号括起来，则所有变量和命令替换将在首次设置 `trap` 时执行。如果命令字符串用单引号括起来，则变量和命令替换直到检测到信号并执行 `trap` 时才进行。

使用命令 `kill -l` 或 `trap -l` 获取所有信号的列表。表 14.6 提供了信号编号及其对应名称的列表。`trap` 最常用的信号有：1) `SIGHUP`（挂起），2) `SIGINT`（中断），3) `SIGQUIT`（退出），4) `SIGTERM`（终止）。

# 格式

```
trap 'command; command' signal-number
trap 'command; command' signal-name
```

## 示例 14.61

```
trap 'rm tmp*; exit 1' 0 1 2 15
trap 'rm tmp*; exit 1' EXIT HUP INT TERM
```

# 说明

当信号 1（挂起）、2（中断）或 15（软件终止）中的任何一个到达时，删除所有 `tmp` 文件并退出。

## 表 14.6 信号编号与信号ᵃ

| 1) SIGHUP | 9) SIGKILL | 17) SIGCHLD | 25) SIGXFSZ |
| 2) SIGINT | 10) SIGUSR1 | 18) SIGCONT | 26) SIGVTALRM |
| 3) SIGQUIT | 11) SIGSEGV | 19) SIGSTOP | 27) SIGPROF |
| 4) SIGILL | 12) SIGUSR2 | 20) SIGTSTP | 28) SIGWINCH |
| 5) SIGTRAP | 13) SIGPIPE | 21) SIGTTIN | 29) SIGIO |
| 6) SIGABRT | 14) SIGALRM | 22) SIGTTOU | 30) SIGPWR |
| 7) SIGBUS | 15) SIGTERM | 23) SIGURG |  |
| 8) SIGFPE | 16) SIGSTKFLT | 24) SIGXCPU |  |

a. 有关 UNIX 信号及其含义的完整列表，请访问 `www.cybermagician.co.uk/technet/unixsignals.htm`。有关 Linux 信号，请访问 `www.comptedoc.org/os/11unix/programming/linux_pgsignals.html`。
