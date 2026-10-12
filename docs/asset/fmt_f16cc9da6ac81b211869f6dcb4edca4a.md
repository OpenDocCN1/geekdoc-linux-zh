
**列表 2-37** 不使用文件描述符的最快方法

我在几乎每个解析文件的脚本中都会使用这种技术，仅仅是因为它在 shell 脚本的生命周期内易于维护。记住，不是如果某人某后需要编辑你的脚本，而是当某人某后需要编辑你编写的最优秀脚本时。他们必须能够理解你做了什么，而不需要费力破解你的代码，或者直接放弃并重写整个脚本。

# 第 2 章 逐行处理文件的 24 种方法

## 命令替换方法的计时

我们还想查看使用 `` `command` `` 相比 `$(command)` 两种命令替换方法之间的计时差异。参见**列表 2-38**，其中方法 4 使用反引号命令替换方法，而方法 5 使用美元括号命令替换方法。

```bash
function while_LINE_line_bottom
{
    # 方法 4
    # 清空 $OUTFILE
    >$OUTFILE
    while LINE='line'
    do
        echo "$LINE" >> $OUTFILE
        :
    done < $INFILE
}

function cat_while_LINE_line_cmdsub2
{
    # 方法 5
    # 清空 $OUTFILE
    >$OUTFILE
    cat $INFILE | while LINE=$(line)
    do
        echo "$LINE" >> $OUTFILE
        :
    done
}
```

**列表 2-38** 命令替换方法

这两种方法的计时数据如**列表 2-39** 所示。

```text
Method 4:
function while_LINE_line_bottom
real 0m31.24s
user      0m13.57s
sys       0m19.70s

Method 5:
function cat_while_LINE_line_cmdsub2
real      0m30.86s
user      0m13.84s
sys       0m20.20s
```

**列表 2-39** 命令替换计时差异

在方法 4 中，命令替换技术使用了反引号 `` `command` ``，它们位于标准键盘的左上角。方法 5 中使用的命令替换技术是默认括号 `$(command)`。两种命令替换方法得到相同的结果，但在实际时间上一种方法略快于另一种。从**列表 2-39** 中每个方法的计时来看，`` `command` `` 方法仅领先 0.38 秒就赢得了实际时间竞赛。但是，看看用户时间和系统时间！反引号方法使用的系统资源更少。然而，这种计时差异非常微小，实际上并不是一个问题。

# 如果使用命令代替文件输入又如何？

我理解这一点。我们并不总是想将命令输出重定向到文件，然后处理该文件。这个额外的步骤会消耗 CPU 周期和磁盘 I/O 时间。当然，我们可以直接将输出管道到下一个命令。

# 第一部分 Shell 脚本基础

## 使用 mail 和 mailx 命令

最常用的通知方法是 `mail` 和 `mailx` 命令。要为邮件添加主题，我们可以添加 `-s` 选项，后跟用引号括起来的主题。这两个命令的基本语法如下：

```bash
mail -s "This is the subject" $MAILOUT_LIST < $MAIL_FILE
```

或

```bash
cat $MAIL_FILE | mail -s "This is the subject" $MAILOUT_LIST
```

或

```bash
mailx -s "This is the subject" $MAILOUT_LIST < $MAIL_FILE
```

或

```bash
cat $MAIL_FILE | mailx -s "This is the subject" $MAILOUT_LIST
```

注意变量 `MAILOUT_LIST` 和 `MAIL_FILE` 的使用。`MAILOUT_LIST` 变量包含一个电子邮件地址列表（或电子邮件别名），用于发送消息的目标。以下示例使用了通过 `mail_alias` 指定 sendmail 别名。`MAIL_FILE` 变量指向包含要发送的消息文本的文件名。

```bash
mail -s "This is the subject" mail_alias > $MAIL_FILE
```

或

```bash
cat $MAIL_FILE | mail -s "This is the subject" mail_alias
```

或

```bash
mailx -s "This is the subject" mail_alias > $MAIL_FILE
```

或

```bash
cat $MAIL_FILE | mailx -s "This is the subject" mail_alias
```

> 注意：并非所有系统都支持 `mailx` 命令，但支持该命令的系统与 `mail` 命令语法相同。为了处理多个 UNIX 平台时安全起见，请始终使用 `mail` 命令。

`MAIL_FILE` 变量指向包含要发送的消息文本的文件名。让我们逐个来看。

假设我们正在监控机器上的文件系统，`/var` 文件系统的使用率已达到 98%，这超过了文件系统视为满的 85% 阈值。系统管理员需要快速收到有关此情况的通知，否则当 `/var` 满时可能会崩溃；根文件系统 `/` 也是如此。在监控 shell 脚本中，定义了一个 `MAIL_FILE` 变量指向文件名 `/tmp/mailfile.out`，即 `MAIL_FILE=/tmp/mailfile.out`。然后我们使用 `/dev/null $MAIL_FILE` 创建了一个零大小的文件。当发现错误时（当 `/var` 使用率达到 88% 时发生），消息会被追加到 `$MAIL_FILE` 中稍后发送。如果发现更多错误，随着 shell 脚本处理每个任务，它们也会追加到文件中。在 shell 脚本结束时，我们可以测试 `$MAIL_FILE` 的大小。如果 `$MAIL_FILE` 中有任何数据，文件大小将大于 0 字节。如果文件为空，则我们什么都不做。

为了说明这个主意，让我们研究**列表 3-1** 中的代码段。

```bash
MAIL_FILE=/tmp/mailfile.out
cat /dev/null $MAIL_LIST="randy.somebody.com 1234567890@mypage_somebody.net"
check_filesystems      # 此函数检查文件系统的百分比
if [ -s $MAIL_FILE ];
then
    mail -s "Filesystem Full" $MAIL_LIST > $MAIL_FILE
fi
```

**列表 3-1** 典型的邮件代码段

在**列表 3-1** 中，我们看到一个定义了 `mail` 命令中使用的 `MAIL_FILE` 和 `MAIL_LIST` 变量的代码段。在这些定义之后，代码执行查找超过阈值文件系统的函数。如果超过阈值，消息将追加到 `$MAIL_FILE` 文件，如下代码段所示：

```bash
FS=/var
PERCENT=98
THISHOST=$$(uname -n)
echo "$THISHOST: $FS is $PERCENT" | tee -a $MAIL_FILE
```

此代码段显示了 `checkfilesystems` 函数。对于我的机器，此 `echo` 语句既会将消息显示在屏幕上，又将其追加到 `$MAIL_FILE` 文件：

```text
yogi:/var is 98%
```
