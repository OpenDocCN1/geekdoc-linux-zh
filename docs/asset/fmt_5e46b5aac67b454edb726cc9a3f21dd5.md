
```
[ OK ] Started Job spooling tools.
Starting Command...
[ OK ] Started Wait for Plymouth Screen to Quit...
Starting Terminate Plymouth Screen...
[ OK ] Started SYSV: Late init script for live image..
[student@krosum ~]$
[student@krosum ~]$ clear
```

### 7. Script 命令

- 记录交互会话。
- 当你想记录整个会话时，在会话中使用此命令，这样你所做的都会被记录，直到你退出会话。
- 要停止记录，输入 `exit`。
- 如果你不指定输出文件名，会话默认保存为文件 `typescript`。

更多细节请参考下面的示例。

```
[student@kosum ~]$ script
Script started, file is typescript
[student@kosum ~]$ date
Tue Mar 24 15:29:16 IST 2020
[student@kosum ~]$ pwd
/home/student
[student@kosum ~]$ whoami
student
[student@kosum ~]$ exit
exit
Script done, file is typescript
[student@kosum ~]$ cat typescript
Script started on Tue 24 Mar 2020 03:29:13 PM IST
[student@kosum ~]$ date
Tue Mar 24 15:29:16 IST 2020
[student@kosum ~]$ pwd
/home/student
[student@kosum ~]$ whoami
student
[student@krosum ~]$ exit
```

帮助文档

- `whoami` 命令返回用户 ID（登录名）。
- 此选项用于获取表头信息。

### 使用选项 -H

此选项用于获取表头信息。

```
$student@krosum-$ who -H
NAME LINE TIME COMMENT
student tty1 2020-03-19 20:22 (:0)
student pts/0 2020-03-24 13:45 (::0)
student pts/1 2020-03-24 14:47 (:0.0)
```

### Who am i

```
$student@krosum-$ who am i
student pts/0 2020-03-24 13:45 (:0.0)
```

如果你只想显示你个人的系统信息，请输入 `who am i`。（注意单词间的空格）。

### Whoami

- `whoami` 命令返回用户 ID（登录名）。
- 如果你以 root 用户登录，`whoami` 将显示 root。
- 如果你以 Student 用户登录，`whoami` 将显示 student。

这等同于以下命令的结果：

```
$student@krosum-$ whoami
student
$student@krosum-$ id -un
student
$student@krosum-$ id -u
student
1000
$student@krosum-$ 
```

`id -un`

`-u` 仅显示登录 ID（整数）。对于 root 用户，这始终为 0 (0)。

### 4. 系统名称 (uname) 命令

`uname` 工具最常用于确定处理器架构、系统主机名以及系统上运行的内核版本。

语法:- `uname --option`

| 选项 | 说明 |
|---|---|
| `-r`(kernel release) | 打印内核版本 |
| `-v` | 打印内核版本 |
| `-m` | 打印机器硬件名称 |
| `-p` | 打印处理器架构 |
| `-i` | 打印硬件平台 |
| `-o` | 打印操作系统名称。在 Linux 系统上为 “GNU/Linux” |
| `-a`(all) | 使用 `-a` 选项时，`uname` 的行为相当于给了 `-snrvmo` 选项。 |

```
[student@krosum ~]$ uname
Linux
[student@krosum ~]$ uname -r
3.9.5-301.fc19.i686
[student@krosum ~]$ uname -s
Linux
[student@krosum ~]$ uname -i
1386
[student@krosum ~]$ uname -p
1686
[student@krosum ~]$ uname -m
1686
[student@krosum ~]$ uname -o
GNU/Linux
```

图 带有选项的 `uname` 命令

### 5. 终端 (tty ) 命令

`tty` 工具用于显示我们正在使用的终端的名称。

```
[student@krosum ~]$ ps [student@krosum ~]$ ps
/dev/pts/0 PID TTY TIME CMD
[student@krosum ~]$ ps 8514 pts/1 00:00:00 bash
PID TTY TIME CMD 8701 pts/1 00:00:00 ps
[student@krosum ~]$ 8206 pts/0 00:00:00 bash [student@krosum ~]$
8700 pts/0 00:00:00 ps /dev/pts/1
[student@krosum ~]
```

我们已经知道 Linux 将一切视为文件。`tty` 是存储在 `/dev` 下的文件。

当我们打开新终端时，端口号会自动递增为 `pts/0`、`pts/1` 等。

### 6. 清屏 (clear) 命令

`clear` 命令清除屏幕并将光标置于顶部。

```
[ OK ] Started Job spooling tools.
Starting Command...
[ OK ] Started Wait for Plymouth Screen to Quit...
Starting Terminate Plymouth Screen...
[ OK ] Started SYSV: Late init script for live image..
[student@krosum ~]$
[student@krosum ~]$ clear
```

### 7. Script 命令

- 记录交互会话。
- 当你想记录整个会话时，在会话中使用此命令，这样你所做的都会被记录，直到你退出会话。
- 要停止记录，输入 `exit`。
- 如果你不指定输出文件名，会话默认保存为文件 `typescript`。

更多细节请参考下面的示例。

```
[student@kosum ~]$ script
Script started, file is typescript
[student@kosum ~]$ date
Tue Mar 24 15:29:16 IST 2020
[student@kosum ~]$ pwd
/home/student
[student@kosum ~]$ whoami
student
[student@kosum ~]$ exit
exit
Script done, file is typescript
[student@kosum ~]$ cat typescript
Script started on Tue 24 Mar 2020 03:29:13 PM IST
[student@kosum ~]$ date
Tue Mar 24 15:29:16 IST 2020
[student@kosum ~]$ pwd
/home/student
[student@kosum ~]$ whoami
student
[student@krosum ~]$ exit
```

```
[student@krosum]-$
[student@krosum]$ whatis passwd
passwd (1) - update user's authentication tokens
sslpassword(l) - compute password hashes
passwd(5) - password file
[student@krosum]-$
[student@krosum]$ man -s 5 password
```

`man` 页的底部部分标题为 SEE ALSO（另需），列出了与该 `man` 页相关的命令或文件。

括号中的数字反映了 `man` 页所在的章节。我们可以使用 `man` 命令配合 `-l` 选项来列出与相同命令或文件名相关的 `man` 页。

例如，要查看 `passwd` 文件的在线 `man` 页，可以使用以下命令：

`man -l passwd`

`passwd (1) -M /usr/man`

`passwd (4) -M /usr/man`

`man -s 4 passwd`

正在重新格式化页面。请稍候...完成
