
列表 1-10 方法 15 在计时测试中位第三

列表 1-10（续）

等待，OCR 文本在这里有一些重叠：

```bash
function while_read_LINE_bottom
{
  # 方法 2

  # 清空 $OUTFILE

  >$OUTFILE

  while read LINE
  do
    echo "$LINE" >> $OUTFILE
  done < $INFILE
}
```

**列表 1-11** 不使用文件描述符的最快方法

我在几乎每个处理文件解析 shell 脚本都会 `true` 这种技术，仅仅是因为 shell 脚本在整个生命周期内易于维护。

## 在循环中使用命令输出

这里展示的技术是一个棒的技巧，可以在不使用管道的情况下执行命令并在循环中使用命令的输出：

```bash
while read LINE
do
  echo <$LINE
done < (command)
```

我知道这看起来有点奇怪。这个技巧是我从我的同事 Brian Beers 那里学到的。我们在这里做的是从循环底部进行输入重定向，在 `done` 循环终止符之后，指定 `done < (command)` 语法。`< (command)` 语法执行命令并将命令的输出指向循环底部。

> 注意：`< (command)` 中 `<` 之间的空格是必须的！

## 邮件通知技术

在本书的 shell 列表中，当发生错误、任务完成以及许多其他原因向用户发送通知是一个好主意。本节展示了其中技术。

### 使用 mail 和 mailx 命令

最常用的通知方法是使用 `mail` 和 `mailx` 命令。这两个命令的基本语法如列表 1-12 所示。

```bash
mail -s "This is the subject" $MAILOUT_LIST < $MAIL_FILE
or
cat $MAIL_FILE | mail -s "This is the subject" $MAILOUT_LIST
or
mailx -s "This is the subject" $MAILOUT_LIST < $MAIL_FILE
or
cat $MAIL_FILE | mail -s "This is the subject" $MAILOUT_LIST
```

列表 1-12 使用 `mail` 和 `mailx` 命令的示例并不是所有系统都支持 `mailx` 命令，但这些系统具有与 `mail` 命令相同的语法。为了在处理多个 UNIX 平台时安全，请始终使用 `mail` 命令。

### 使用 sendmail 命令发送出站邮件

在我工作过的一家店里，我无法从名为 `root` 的用户发送出站邮件。`from` 字段必须是一个被邮件服务器识别的有效邮箱地址，`root` 是无效的。为了解决这个问题，我将使用的命令从 `mail` 改为 `sendmail`。`sendmail` 命令允许我们添加 `-f` 来验证字段中的有效邮箱地址。在 AIX、HP-UX、Linux 和 OpenBSD 上，`sendmail` 命令位于 `/usr/bin/sendmail`，但在 SunOS 上位置更改为 `/usr/lib/sendmail`。查看列表 11-3 中的 `send_notification` 函数。

```bash
function send_notification {
  if [ -s $MAIL_FILE -a "$MAILOUT" = "TRUE" ];
  then
    case ($uname) in
      AIX|HP-UX|Linux|OpenBSD) SENDMAIL="/usr/sbin/sendmail"
      ;
      SunOS)
        SENDMAIL="/usr/lib/sendmail"
      ;
    esac
    echo "\nSending email notification"
    $SENDMAIL -f root@$HOSTNAME < $MAIL_FILE
  fi
}
```

列表 1-13 `send_notification` 函数

`mail` 和 `mailx` 命令也支持使用 `-r` 切换来指定 `from` 字段，如列表 1-14 所示。

```bash
mail -r root@$HOSTNAME -s "This is the subject" < $MAIL_FILE
or
cat $MAIL_FILE | mail -r root@$HOSTNAME -s "This is the subject"
or
mailx -r root@$HOSTNAME -s "This is the subject" < $MAIL_FILE
or
cat $MAIL_FILE | mailx -r root@$HOSTNAME -s "This is the subject"
```

列表 1-14 使用 `mail` 和 `mailx` 指定 `from` 字段

这两种技术都应该让你快速将消息发出去。

## 创建进度指示器

当用户因为长时间运行而被迫等待时，给用户一些反馈是一个极佳的主意。本节介绍进度指示器。

### 点序列

`echo` 命令在屏幕上打印一个点，而 `\c` 指定在同一行内继续而不进行回车。为了制作一系列点，我们将在循环中使用嵌套 `while` 循环，并在每个点之间留出一些睡眠时间。我们将使用一个无限循环的 `while` 循环，在屏幕上打印每个点之间睡眠 10 秒：

```bash
while true
do
    echo -n .
    sleep 10
done
```

### 旋转线

列表 1-15 所示的 `rotate_line` 函数在进程运行时看起来像是一个旋转的线。

```bash
function rotate_line
{
    INTERVAL=1      # 每次“旋转”之间的睡眠时间
    TCOUNT=0         # 旋转计数器

    while do              # 直到函数被杀死为止循环
        TCOUNT=$(expr $TCOUNT + 1)

        case $TCOUNT in
            "1") echo -n "/"
                sleep $INTERVAL
                ;;
            "2") echo -n "|"
                sleep $INTERVAL
                ;;
            "3") echo -n "-"
                sleep $INTERVAL
                ;;
            "4") echo -n "\\"
                sleep $INTERVAL
                ;;
            *) TCOUNT=0; # 重置计数器为“0”
        esac
    done
}
```

在 shell 脚本中使用 `rotate_line`，请使用列表 1-16 所示的技术启动并停止它。

```bash
#######################################
###### 主部分
#######################################

rotate_line & # 在后台运行函数

ROTATE_PID=$! # 获取后台进程的 PID
/usr/local/bin/my_time_consuming.ksh

## 停止旋转函数

kill -9 $ROTATE_PID

## 清除残留的行
clear
```

## 时间

`elapsed_time` 函数需要秒作为输入，并输出小时、分钟和秒表示的时间。列表 1-17 显示了 `elapsed_time` 函数。

```bash
function elapsed_time
{
SEC=$1
(( SEC < 60 )) && echo "Elapsed time: $SEC seconds"
(( SEC >= 60 && SEC < 3600 )) && echo "Elapsed time: $((SEC / 60 )) min $((SEC % 60 )) sec"
(( SEC > 3600 )) && echo "Elapsed time: $((SEC / 3600 )) hr $((((SEC % 3600) / 60 )) sec"
}
```

列表 1-17 `elapsed_time` 函数

使用 `elapsed_time` 函数的示例如下：

```bash
elapsed_time 6465
[Elapsed time: 1 hr 47 min 45 sec]
```

## 处理记录文件
