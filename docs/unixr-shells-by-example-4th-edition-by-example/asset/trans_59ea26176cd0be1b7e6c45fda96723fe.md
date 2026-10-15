

1. 出错时以代码 2 退出。否则以代码 0 退出。这使得可以使用退出代码来查看主机是否存活。

此程序 intended for use in network testing, measurement, and management. 因为它可能给网络带来负载，在正常操作期间或从自动化脚本中使用 ping 是不明智的。

## ps—reports process status

```
ps [ -acdefj ] [ -g grplist ] [ -p proclist ]
[ -s sidlist ] [ -t term ] [ -u uidlist ]
```

ps 打印有关活动进程的信息。没有选项时，ps 打印与控制终端关联的进程的信息。输出仅包含进程 ID、终端标识符、累计执行时间和命令名。否则，显示的信息由选项控制。ps 选项在 AT&T 和 Berkeley 类型的 UNIX 版本中并不相同。

### EXAMPLE A.42

```
1  ps -aux | grep "^linda"    # ucb
2  ps -ef | grep "A ^linda"   # at&t
```

### EXPLANATION

- 1 打印所有正在运行的进程并将输出通过管道传递给 grep 程序，并仅打印由用户 linda 拥有的进程，其中 linda 位于每行的开头。 （UCB 版本）
- 2 与第一个示例相同，只是 AT&T 版本。

## pstree—displays a tree of processes

```
pstree [-a] [-c] [-h] [-l] [-n] [-p] [-u] [-G|-U][pid|user]
pstree -V
```

pstree 将正在运行的进程显示为树。树的根为 pid 或如果省略 pid 则为 init。如果指定了用户名，则显示由该用户拥有的进程为根的所有进程树。pstree 通过将它们放在方括号中并在前面加上重复次数来视觉合并相同的分支，例如：

```
init--+--getty
       |-getty
       |-getty
       |-getty

becomes

init---+--4[ getty ]
```

## pwd—displays the present working directory name

## quota—displays users' disk usage and limits

```
quota [ -guvv | q ]
quota [ -uvv | q ] user
quota [ -guv | q ] group
```

quota 显示用户的磁盘使用情况和限制。默认情况下，仅打印用户配额。

- -g 为用户所属的组打印组配额。
- -u 一个可选标志，等同于默认值。
- -v 在未分配存储的文件系统上显示配额。
- -q 打印更简洁的消息，仅包含使用量超过配额的文件系统的信息。

## rcp—remote file copy

```
rcp [ -p ] filename1 filename2
rcp [ -pr ] filename...directory
```

rcp 命令以以下形式在机器之间复制文件：

```
remotehostname:path
user@hostname:file
user@hostname.domainname:file
```

### EXAMPLE A.43

- 1 rcp dolphin:filename /tmp/newfilename
- 2 rcp filename broncos:newfilename

### EXPLANATION

- 1 将文件 filename 从远程机器 dolphin 复制到本机上的 /tmp/newfilename。
- 2 将文件 filename 从本机复制到远程机器 broncos 并命名为 newfilename。

## rdate—gets the date and time via the network

```
rdate [-p] [-s] [host...]
```

rdate 使用 TCP 通过 RFC 868 中描述的协议检索另一台机器的当前时间。使用 -p 选项，rdate 打印从远程机器检索到的时间。这是默认模式。使用 -s 选项，rdate 将本地系统时间设置为从远程机器检索到的时间。只有超级用户可以重置时间。每个系统的返回时间采用 ctime(3) 格式。

### EXAMPLE A.44

```
1 rdate homebound atlantis
(Output)
[homebound] Tue Jan 18 20:35:41 2000
[atlantis] Tue Jan 18 20:36:19 2000
```

## rgrep—a recursive, highlighting grep program

rgrep [ options] pattern [file] .....

rgrep 与 grep 和 egrep 不同，可以递归下降目录。 在 UNIX 系统上执行此类搜索的传统方法利用 find 命令与 grep 结合使用。使用 rgrep 可获得更好的性能。另请参阅 xargs 命令。

### COMMAND-LINE OPTIONS:

| -? | Additional help (use -? to avoid shell expansion on some systems). |
| -c | Count matches. |
| -h | Highlight match (ANSI-compatible terminal assumed). |
| -H | Output match instead of entire line containing match. |
| -i | Ignore case. |
| -l | List filename only. |
| -n | Print line number of match. |
| -F | Follow links. |
| -r | Recursively scan through directory tree. |
| -N | Do NOT perform a recursive search. |
| -R pat | Like -r except that only those files matching pat are checked. |
| -v | Print only lines that do NOT match the specified pattern. |
| -x ext | Check only files with extension given by ext. |
| -D | Print all directories that would be searched. This option is for debugging purposes only. No file is grepped with this option. |
| -W len | Lines are len characters long (not newline terminated). |

