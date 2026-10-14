
```
Reply from 207.171.0.111: bytes=32 time=176ms TTL=247
Reply from 207.171.0.111: bytes=32 time=157ms TTL=247
Reply from 207.171.0.111: bytes=32 time=156ms TTL=247
Reply from 207.171.0.111: bytes=32 time=150ms TTL=247
```

## printenv

**目的：** `printenv` 将打印所有当前环境变量。

**示例：** `printenv`. 这里是一些示例 `printenv` 输出：

```
HOME=/home/bwagner
HZ=100
LOGNAME=bwagner
MAIL=/var/mail/bwagner
PATH=/usr/bin::/usr/local/bin
SHELL=/sbin/bin
TERM=ansi
TZ=US/Pacific
```

要了解更多关于 `printenv` 的信息，请参阅第 5 章。

## ps

**目的：** `ps` 报告当前进程的状态。

**示例：** `ps -a`. 这打印所有当前进程。这里是一些示例 `ps` 输出：

350

## 录 A > 命令参考

| PID | TTY | TIME | CMD |
| :--- | :--- | :--- | :--- |
| 9757 | pts/12 | 0:00 | telnet |
| 3159 | pts/23 | 0:02 | pine |
| 9694 | pts/9 | 0:00 | sh |
| 8463 | pts/7 | 0:00 | sh |
| 2503 | pts/4 | 0:00 | tcsh |
| 8102 | pts/2 | 0:00 | csh |
| 9741 | pts/0 | 0:01 | telnet |
| 9753 | pts/12 | 0:00 | csh |
| 9161 | pts/1 | 0:00 | sh |

```
pwd
```

**目的：** `pwd` 显示当前目录名称。

**示例：** `pwd`. 这打印当前目录名。

```
rcp
```

**目的：** `rcp` 从远程主机复制文件。

**示例：** `rcp target:/home/file.txt`. 这从主机复制 `file.txt` 并给出本地文件名。

```
rlogin
```

**目的：** `rlogin` 代表远程登录。`rlogin` 在所有主机上自动登录一致的用户 ID。

**示例：** `rlogin target`. 在你的机器与主机之间启动远程会话。

```
rm
```

**目的：** `rm` 删除指定文件。

**示例：** `rm myfile.txt`. 这删除 `myfile.txt`。要了解更多关于 `rm` 的信息，请参阅第 6 章。

```
rmdir
```

**目的：** `rmdir` 删除空目录。

**示例：** `rmdir /directory`. 这删除目录。要了解更多关于 `rmdir` 的信息，请参阅第 6 章。

351

## sh

**目的：** `sh` 是 UNIX shell。

**示例：** `sh`. 这启动 shell。要了解更多关于 shells 的信息，请参阅第 5 章。

## sort

**目的：** `sort` 按行排序文本。

**示例：** `sort myfile.txt`. 这对 `myfile.txt` 的内容进行排序。

## stty

**目的：** `stty` 显示终端设置。

**示例：** `stty [options]`. 有许多选项。请参阅 `stty` 页获取更多信息。

## tail

**目的：** `tail` 默认显示指定文件的最后几行。

**示例：** `tail myfile.txt`. 这显示 `myfile.txt` 的最后几行。你也可以指定要显示的行数，例如 `tail -50 myfile.txt` 会打印最后的 50 行。

## talk

**目的：** `talk` 允许你与另一个用户聊天。

**示例：** `talk bwagner`. 这将聊天。

## telnet

**目的：** `telnet` 允许你与其他主机进行远程会话。

**示例：** `telnet 207.171.0.111`. 这建立到 `207.171.0.111` 的连接。要了解更多关于 `telnet` 的信息，请参阅第 21 章。

## traceroute

**目的：** `traceroute` 跟踪数据包从 A 点（你的机器）到 B 点（远程主机）的路径。这通常用于确定网络故障。

**示例：** `traceroute mcp.com`. 这是一些 `traceroute` 输出：

```
traceroute to mcp.com (204.95.236.226), 30 hops, 40 byte packets
1 cisco-t3.pacific.net (207.171.0.111) 3 ms 3 ms 2 ms
2 206.171.134.33 (206.171.134.33) 9 ms 4 ms 4 ms
3 edge1-fe8-0-islsan03.pbi (206.132.130) 5 ms 4 ms 4 ms
4 165.87.316 (165.87.316) 6 ms 5 ms 5 ms
5 165.87.32.109 (165.87.32.109) 16 ms 68 ms 11 ms
6 165.87.230.202 (165.87.230.202) 19 ms 16 ms 17 ms
7 165.87.33.131 (165.87.33.131) 18 ms 18 ms 18 ms
8 mae-west.nap.net (198.32.136.163) 18 ms 21 ms
9 207.112.247.157 (207.112.247.157) 94 ms 91 ms 94 ms
10 207.112.247.153 (207.112.247.153) 97 ms 108 ms 112 ms
11 * chi-iquest.net (206.54.225.250) 96 ms 96 ms 101 ms
12 204.180.50.9 (204.180.50.9) 104 ms 98 ms 101 ms
13 iq-ss6.iquest.net (206.246.140.166) 97 ms * 102 ms
```

## tty

**目的：** `tty` 显示当前终端的名称。

**示例：** `tty`.

## uname

**目的：** `uname` 将获取系统信息，包括架构、操作系统和处理器类型。

**示例：** `uname -a`. 这里是一些示例输出：

```
SunOS wagajag 5.6 Generic sun4 sparc SUNW,Ultra-1
```

## uniq

**目的：** `uniq` 将查找并删除指定文件中的重复行。

**示例：** `uniq myfile.txt`.

## uptime

**目的：** `uptime` 报告系统运行了多久。

**示例：** `uptime`. 这里是一些示例 `uptime`：

9:31pm up 4 day(s), 20:36, 14 users, load average: 0.00, 0.01, 0.02

## vi

**目的：** `vi` 是一个文本编辑器。

**示例：** `vi myfile.txt`. 这启动 `vi` 来编辑 `myfile.txt`。要了解更多关于 `vi` 的信息，请参阅第 8 章。

## wall

**目的：** `wall` 将指定消息发送到所有终端。

**示例：** `work sucks!!` 这将在所有终端打印以下消息：

work sucks!!

## wc

**目的：** `wc` 将统计并显示指定文件的字节数、单词和行数。

**示例：** `wc myfile.txt`. 这将显示 `myfile.txt` 的统计数据。

## whatis

**目的：** `whatis` 显示指定命令的简短描述。

**示例：** `whatis whatis`. 这将显示 `whatis` 的 man 页描述。输出如下：

whatis (1) - display manual page descriptions

## whereis

**目的：** `whereis` 定位文件。

**示例：** `whereis traceroute`. 这启动对 `traceroute` 文件的搜索。

354

# who

**用途：** `who` 显示当前登录用户的统计信息。

**示例：** `who`. 这里是一些示例输出：
