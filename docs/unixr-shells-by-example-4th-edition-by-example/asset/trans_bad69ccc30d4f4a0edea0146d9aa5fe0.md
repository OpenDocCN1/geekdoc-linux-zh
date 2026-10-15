

## 示例 11.23

```
1  $ vi
   [1] + Stopped        # vi
2  $ sleep 25&
   [2] 4538
3  $ jobs
   [2] + Running        # sleep 25&
   [1] - Stopped        # vi
4  $ jobs -l
   [2] + 4538  Running   # sleep 25&
   [1] - 4537  Stopped   # vi
5  $ fg %1
```

## 解释

- 1. 调用 vi 编辑器后，可以按 ^Z（Ctrl-Z）挂起 vi 会话。编辑器将在后台被挂起，出现 Stopped 消息后，shell 提示符会立即出现。
- 2. 命令末尾的与符号（&）使 sleep 命令以参数 25 在后台执行。符号 [2] 表示这是第二个在后台运行的作业，该作业的 PID 为 4538。
- 3. jobs 命令显示当前后台中的作业。
- 4. 带 -l 选项的 jobs 命令显示后台中运行的进程（作业）及这些作业的 PID 编号。
- 5. fg 命令后跟百分号和作业编号，将该编号的作业调入前台。如果没有编号，fg 会将最近放到后台的作业调回前台。

## 11.7 元字符

元字符是用来表示自身以外含义的特殊字符。表 11.6 列出了一些常见的 Korn Shell 元字符及其功能。

### 表 11.6 Korn Shell 元字符

| 命令 | 功能 |
| --- | --- |
| \ | 对后面的字符进行字面解释 |
| & | 后台处理 |
| ; | 命令分隔符 |
| $ | 变量替换 |
| ? | 匹配单个字符 |

### 表 11.6 Korn Shell 元字符（续表）

| 命令 | 功能 |
|---|---|
| [abc] | 匹配字符集合中的一个 |
| [!abc] | 匹配不在字符集合中的一个 |
| * | 匹配零个或多个字符 |
| (cmds ) | 在子 shell 中执行命令 |
| {cmds} | 在当前 shell 中执行命令 |

## 示例 11.26

```
1 $ ls -d s
all files are displayed
abc abc122 abc2 file1.bak file2.bak nonsense nothing one
abc1 abc123 file1 file2 none noone

2 $ print hello \
> there        # The carriage return is escaped
hello there

3 $ rusers&
# Process the rusers command in the background
[1] 4334
$

4 $ who; date; uptime   # Commands are executed one at a time
ellie console Feb 10 10:46
ellie tty p0 Feb 15 12:41
ellie tty p1 Feb 10 10:47
ellie tty p2 Feb 5 10:53
Mon Feb 15 17:16:43 PST 2004
5:16pm up 5 days, 6:32, 1 user, load average: 0.28, 0.23, 0.01

5 $ print $HOME        # The value of the HOME variable is printed
/home/jody/ellie

6 $ print $LOGNAME     # The value of the LOGNAME variable is printed
ellie

7 $ ( pwd; cd / ; pwd )
/home/jody/ellie
/
```

## 示例 11.26（续）

```
$ pwd
/home/jody/ellie

8 $ { pwd; cd /; pwd; }
/home/jody/ellie
/
$ pwd
/

9 $ { date; pwd; ls } > outfile
$ cat outfile
Mon Feb 15 15:56:34 PDT 2004
/home/jody/ellie
foo1
foo2
foo3
```

## 解释

- 1 星号匹配当前目录中的所有文件。（ls 命令的 -d 选项可防止子目录内容被显示出来。）
- 2 反斜杠转义换行符，使命令行能够继续在下一行输入。
- 3 与符号（&）使 rusers 程序在后台执行；shell 提示符立即返回。两个进程将同时运行。
- 4 每个命令之间用分号分隔。每条命令将依次执行。
- 5 如果变量前有美元符号，shell 将执行变量替换。环境变量 HOME 的值被显示出来。HOME 变量包含用户主目录的完整路径名。
- 6 同样，美元符号位于变量名之前。LOGNAME 变量的值是用户的登录名。
- 7 圆括号表示括号内的命令将在子 shell 中执行。cd 命令内置于 shell 中，因此每个被调用的 shell 都有自己的 cd 副本。pwd 命令打印当前工作目录。/home/jody/ellie 在使用 cd 命令切换到根目录后，pwd 命令显示新目录为根目录。子 shell 退出后，父 shell 中 pwd 命令的输出表明，目录仍与进入子 shell 之前一样，设置为 /home/jody/ellie。

