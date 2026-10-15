

## 13.17.1 exec 命令和重定向

exec 命令可用于用新程序替换当前程序，而无需启动新进程。标准输出或输入可通过 exec 命令更改，而无需创建子 shell。（参见表 13.24。）如果使用 exec 打开文件，后续的读命令将使文件指针每次向下移动一行，直到文件末尾。必须关闭文件才能重新从开头读取。然而，如果使用 cat 和 sort 等 UNIX 工具，操作系统会在每个命令完成后关闭文件。

### 表 13.24 exec 命令

| 命令 | 其作用 |
|---|---|
| exec ls | ls 在 shell 位置执行。当 ls 完成后，启动它的 shell 不会返回。 |
| exec < filea | 打开 filea 以供标准输入读取。 |
| exec > filex | 打开 filex 以供标准输出写入。 |
| exec 3< datfile | 打开 datfile 作为文件描述符 3 以供输入读取。 |
| sort <&3 | Datfile 被排序。 |
| exec 4>newfile | 打开 newfile 作为文件描述符 (fd) 4 以供写入。 |
| ls >&4 | ls 的输出被重定向到 newfile。 |
| exec 5>&4 | 使 fd 5 成为 fd 4 的副本。 |
| exec 3<&- | 关闭 fd 3。 |

### 示例 13.84

```
1 $ exec date
Thu Oct 14 10:07:34 PDT 2004
<login prompt appears if you are in your login shell>
2 $ exec > temp
$ ls
$ pwd
$ echo Hello
3 $ exec > /dev/tty
4 $ echo Hello
Hello
```

### 解释

- 1 exec 命令在当前 shell 中执行 date 命令（不 fork 子 shell）。由于 date 命令是在当前 shell 的位置执行，当 date 命令退出时，shell 终止。如果是从 TC shell 启动的 bash shell，bash shell 将退出并出现 TC shell 提示符。如果你在登录 shell 中尝试此操作，你将被注销。如果你正在交互式 shell 窗口中工作，窗口将退出。
- 2 exec 命令为当前 shell 打开标准输出到 temp 文件。ls、pwd 和 echo 的输出将不再显示在屏幕上，而是写入 temp。（参见图 13.2。）
- 3 exec 命令重新打开标准输出到终端。现在，输出将显示在屏幕上，如第 4 行所示。
- 4 标准输出已重新定向回终端 (/dev/tty)。

![](img/60a0b5d254bd6007403850f972cbfad8_884_0.png)

### 示例 13.85

```
1 > bash
2 $ cat doit
pwd
echo hello
date
3 $ exec < doit
/home/homebound/ellie/shell
hello
Thu Oct 14 10:07:34 PDT 2004
4 >
```

### 解释

- 1 从 TC shell 提示符启动 bash。（这样做是为了当 exec 命令退出时，用户不会被注销。）
- 2 显示名为 doit 的文件的内容。
- 3 exec 命令将标准输入打开到名为 doit 的文件。输入从文件而不是键盘读取。文件 doit 中的命令在当前 shell 的位置执行。当最后一个命令退出时，shell 也退出。
- 4 bash shell 在 exec 命令完成后退出。TC shell 提示符出现。它是父 shell。如果你是在登录 shell 中等待 exec 完成，你将被注销；如果在窗口中，窗口将消失。

### 示例 13.86

```
1 $ exec 3> filex
2 $ who >&3
3 $ date >&3
4 $ exec 3<&-
5 $ exec 3<filex
6 $ cat <&3
   ellie    tty1   Jul 21 09:50
   ellie    ttyv0  Jul 21 11:16  (:0.0)
   ellie    ttyv0  Jul 21 16:49  (:0.0)
   Wed Jul 21 17:15:18 PDT 2004
7 $ exec 3<&-
8 $ date >&3
date: write error: Bad file descriptor
```

## 13.18 管道

管道将管道符号左侧命令的输出取出并发送到管道符号右侧命令的输入。管道线可以包含一个以上的管道。

示例 13.87 中命令的目的是统计登录人数（who），将命令的输出保存到文件（tmp），使用 wc -l 命令统计 tmp 文件中的行数（wc -l），然后删除 tmp 文件（即找出登录人数）。

### 示例 13.87

```
1 $ who > tmp
2 $ wc -l tmp
4 tmp
3 $ rm tmp

# Using a pipe saves disk space and time.

4 $ who | wc -l
4
5 $ du .. | sort -n | sed -n '5p'
1980 ..
6 $ ( du / | sort -n | sed -n '5p' ) 2> /dev/null
1057747 /
```

### 解释

- 1 who 命令的输出被重定向到 tmp 文件。
- 2 wc -l 命令显示 tmp 中的行数。

![](img/60a0b5d254bd6007403850f972cbfad8_886_0.png)

图 13.3 exec 和文件描述符。

