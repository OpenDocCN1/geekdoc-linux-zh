
# ps

`alex 3303 0.0 0.2 2476 616 p/0 R Jul31 0:00 -ps -u`

`-ef` 选项导致 `ps` 以“ASCII 艺术进程树”的形式显示主页。其他进程的子进程将显示在其父进程下方，使得进程层级结构（或树形结构）更加可见。

```
$ ps -ef --forest

UID PID PPID CTIME TIME CMD

root 1 0 Jul22 ? 00:00:00 init

root 2 1 Jul22 ? 00:00:00 [kevent]

root 785 1 Jul22 ? 00:00:00 /usr/sbin/apmind -p 10 -w 5 -W -P

root 839 1 Jul22 ? ?00:00:01 /usr/sbin/sshd

root 3305 39 Aug 01 ? 00:00:00 /usr/sbin/sshd

alex 3307 35 Aug 01 ? 00:00:00 /usr/sbin/sshd

alex 3308 37 Aug 01 pts/1 00:00:00 -bash

alex 3774 38 Aug 01 pts/1 00:00:00 -ps -ef --forest

root 1040 1 Jul22 ? 00:00:00 login

root 3351 1040 Aug 01 tty2 00:00:00 -bash

root 3402 3351 Aug 01 tty2 00:00:00 make modules

root 3416 3402 Aug 01 tty2 00:00:00 make -C drivers CFLA

- 3764 3716 Aug 01 tty2 00:00:00 make -C scsi mod

root 3773 3764 Aug 01 tty2 00:00:00 -ld -melf elf_13
```

接下来的命令序列展示了如何使用 `ps` 来确定后台运行进程的 `PID` 号，以及如何使用 `kill` 命令终止该进程。在这种情况下，没有必要使用 `ps`，因为 `shell` 会显示后台进程的 `PID` 号。`ps` 工具用于验证 `PID` 号。

第一个命令在后台执行。`shell` 会显示该进程的作业号和 `PID` 号，然后是命令提示符。

```
$ find ~ -name memo -print > memo.out &
[1] 3343
```

接下来，通过 `ps` 确认后台任务的 `PID`。如果你从先不知道这个数字，使用 `ps` 是找到它的唯一方法。

```
$ ps

PID TTY TIME CMD

3308 pts/1 00:00:00 bash

3343 pts/1 00:00:00 find

3344 pts/1 00:00:00 ps
```

最后，使用 `kill`（第 693 页）终止进程。

```
$ kill 3343
$ RETURN
[1]+ Terminated
find ~ -name memo -print > memo.out
```

# rcp

将一个或多个文件复制到远程系统或从中复制

* `rcp [options] source-file destination-file`
* `rcp [options] source-file-list destination-directory`

`rcp` 工具在可以通过网络通信的两个系统之间复制一个或多个普通文件。

## rcp 不安全

`rcp` 工具使用基于主机的信任机制（这是不安全的）来授权文件复制。在可用时，请使用 `scp`（第 758 页）。

## 参数

`source-file`、`source-file-list` 和 `destination-file` 是普通文件的路径名，而 `destination-directory` 是目录文件的路径名。不包含冒号（`:`）的路径名是本地系统上的文件名称。格式为 `name@host:path` 的路径是名为 `host` 的远程系统上的名称。该路径相对于用户名的家目录（除非 `path` 是绝对路径）。当你省略目标中的 `name@` 部分时，相对路径相对于执行 `rcp` 命令的用户所在主机上的家目录。

像 `cp` 一样，`rcp` 有两种操作模式：第一是将一个文件复制到另一个，第二是将一个或多个文件复制到目录。`source-file`[-`list`] 是 `rcp` 将要复制的文件名列表，`destination-file` 是分配给复制副本的文件名，或者 `destination-directory` 是 `rcp` 将复制的文件放入的的目录名称。当 `rcp` 将文件复制到 `destination-directory` 时，文件将保持其原始文件名。

* `-p` (preserve) 将每个副本的修改时间和文件权限设置为与 `source-file` 匹配。当你不使用 `-p` 时，`rcp` 对文件使用创建掩码（`umask`；见第 810 页）。
* `-r` (recursive) 复制目录及其子目录。

# 注意事项

`source-file`、`source-file-list` 和 `destination-file` 是普通文件的路径名，而 `destination-directory` 是目录文件的路径名。不包含冒号（`:`）的路径名是本地系统上的文件名称。格式为 `name@host:path` 的路径是名为 `host` 的远程系统上的名称。该路径相对于用户名的家目录（除非 `path` 是绝对路径）。当你省略目标中的 `name@` 部分时，相对路径相对于执行 `rcp` 命令的用户所在主机上的家目录。

像 `cp` 一样，`rcp` 有两种操作模式：第一是将一个文件复制到另一个，第二是将一个或多个文件复制到目录。`source-file`[-`list`] 是 `rcp` 将要复制的文件名列表，`destination-file` 是分配给复制副本的文件名，或者 `destination-directory` 是 `rcp` 将复制的文件放入的目录名称。当 `rcp` 将文件复制到 `destination-directory` 时，文件将保持其原始文件名。

* `-p` (preserve) 将每个副本的修改时间和文件权限设置为与 `source-file` 匹配。当你不使用 `-p` 时，`rcp` 对文件使用创建掩码（`umask`；见第 810 页）。
* `-r` (recursive) 复制目录及其子目录。

# rlogin

登录远程系统

`rlogin [options] remote-system`

`rlogin` 工具通过网络在远程系统上建立登录会话。

## rlogin 不安全

`rlogin` 工具使用基于主机的信任机制（这是不安全的）来授权你的登录。或者，它以明文形式通过网络发送你的密码，这是一种不安全的做法。可用时，请使用 `ssh`（第 773 页）。

## 参数

`remote-system` 是本地系统可以通过网络访问的系统名称。

## 选项

* `-l` `username` (login) 以指定 `username` 的身份登录远程系统。

## 注意事项

如果远程系统上的 `/etc/hosts.equiv` 文件指定了本地系统的名称，远程系统将不会提示你输入密码。列在 `/etc/hosts.equiv` 文件中的系统被认为是安全的本地系统。

另一种指定信任关系的方法是基于用户的。每个用户的家目录都可以包含一个名为 `~/.rhosts` 的文件，其中保存了受信任的远程系统和用户列表。参见“示例”获取 `.rhosts` 示例。

## rm

删除文件（删除链接）

```
rm [options] file-list
```

`rm` 工具用于删除指向一个或多个文件的硬链接和/或符号链接。当你删除一个文件的最后一个硬链接时，该文件会被删除。

### 在配合通配符使用 rm 时要小心

**注意** 由于你可以使用一个命令删除大量文件，请务必谨慎使用 `rm`，特别是在你处理具有歧义的文件引用时。如果你对使用歧义文件引用的 `rm` 命令的效果有疑，请先对相同的文件引用使用 `echo` 命令，并评估其生成的生成列表。或者，你可以使用 `--interactive` 选项。

### 参数

`file-list` 是 `rm` 删除的文件列表。

### 选项

接受第 587 页描述的常用选项。

当你想要删除一个以连字符（`-`）开头的文件时，必须防止 `rm` 将文件名解释为选项。一种方法是在文件名之前提供特殊选项 `--`。此选项告诉 `rm` 后面不再不再有更多选项：跟随其后的任何参数都是文件名，即使它们看起来像选项。

### 使用 shred 安全地删除文件

**安全** 使用 `rm` 并不会安全地删除文件——用 `rm` 删除的文件是可以恢复的。使用 `shred` 工具可以更安全地删除文件。请参见第 634 页的“擦除文件”示例，了解另一种更安全的删除文件的方法。

### 示例

以下命令分别删除了工作目录和另一个目录中的文件：

```
$ rm rm memo
$ rm letter memol memo2
$ rm /home/jenny/temp
```

下一个示例在删除工作目录及其子目录中的每个文件之前会询问用户：

```
$ rm -ir
```

此命令对于删除包含特殊字符（尤其是`空格`、`制表符`和`换行符`）的文件非常有用。（你不应该创建包含这些字符的文件名，但可能会意外发生。）

## rmdir

删除目录

```
rmdir directory-list
```

`rmdir` 工具用于删除空目录。

### 参数

`directory-list` 是 `rmdir` 删除的空目录路径列表。

### 选项

接受第 587 页描述的常用选项。

* `--ignore-fail-on-empty`

  抑制 `rmdir` 在因目录为空而失败时通常显示的消息。配合 `--parents` 选项，当 `rmdir` 发现非空目录时将不会退出。

* `--parents -p`

  删除一系列嵌套的空目录，从子目录开始。

* `--verbose -v`

  在删除目录时显示目录名称。

### 注意事项

如果你需要删除非空目录及其内容，请配合 `-f` 选项使用 `rm` 工具。

### 示例

以下命令删除了工作目录下的空目录 `literature` 目录：

```
$ rmdir literature
```

下一个命令使用绝对路径删除 `letters` 目录：

```
$ rmdir /home/jenny/letters
```

最后一个命令在假设路径中命名的其他目录外，这些目录都是空的情况下，删除 `letters`、`march` 和 `05` 目录：

```
$ rmdir --parents letters/march/05
```

## rsh

在远程系统上执行命令

```
rsh [option] host [command-line]
```

`rsh` 工具通过在远程系统上启动 `shell` 来在主机上运行命令行。如果没有提供命令行，`rsh` 会调用 `login`，这会将你登录到远程系统。

### rsh 不安全的

`rsh` 工具使用基于主机的信任机制来授权你的登录，这种机制是不安全的。或者，它会将你的密码以明文形式通过网络发送，这并不是一种安全的做法。可用时请使用 `ssh`（第 773 页）。

### 参数

`host` 是远程系统的名称。`rsh` 工具在远程系统上运行命令行。你必须对命令行中的特殊字符加引号，以防止它们在传递给 `rsh` 之前被本地 `shell` 展开。

### 选项

* `-` `username` (login)

  以 `username` 指定的用户身份登录远程系统。

### 注意事项

如果远程系统上名为 `/etc/equiv` 的文件指定了本地系统的名称，则远程系统将不会提示你输入密码。另一种指定登录用户的方法请参见 `login` 下的“示例”。

### 示例

在第一个示例中，`rsh` 使用了目录：

```
$ rsh ls
```

下一个示例中对字符 (>) 加了引号以便其被解释：

```
$ rsh ls > file
```

在最后一个示例中，`rsh` 使用了登录：

```
$ rsh -l user ls
```

## scp

安全地将一个或多个文件拷贝到远程系统

```
scp [[user@]@from-host:]source-file [[user@]@to-host:]destination-file
```

安全拷贝工具通过网络将普通文件或目录从一个系统拷贝到另一个系统。该工具使用 `ssh` 传输文件并具有相同的身份验证机制；因此它提供了与 `ssh` 相同的安全性。`scp` 工具在需要时提示密码。

### 参数

`from-host` 是源系统名称，`to-host` 是目标系统名称。如果未指定，`scp` 假设为本地系统。系统上的用户默认为执行命令的本地用户；你可以通过 `user@` 指定不同的用户。`scp` 工具允许在两个远程系统之间进行拷贝。

`source-file` 是要拷贝的文件，`destination-file` 是生成的拷贝文件。你可以使用相对路径或绝对路径指定文件或目录。相对路径相对于指定的或隐含的用户主目录。当 `source-file` 是目录时，必须使用 `-r` 选项拷贝其内容。

### 选项

* `-p` (preserve)

  保留原始文件的修改时间和访问时间以及权限。

* `-q` (quiet)

  不显示进度条。

* `-r` (recursive)

  递归拷贝目录树。

* `-v` (verbose)

  显示关于连接和传输的调试信息。当情况不符合预期时，此选项非常有用。

### 注意事项

`scp` 工具是 `OpenSSH` 套件中安全连接工具之一。请参见第 774 页的“注意事项”关于 `OpenSSH` 安全性的讨论。有关在使用 首次连接到远程系统时可能获得的消息，请参阅第 774 页的“首次连接服务器的消息”。

你可以与本地系统或在两个远程系统之间进行拷贝。确保你对拷贝的文件具有读取权限，对目标目录具有写入权限。

你必须对远程路径中的通配符字符（如 `*`）加引号，以便由远程系统上的 `shell` 解释而非本地 `shell`。

与 `cp` 类似，如果在运行 `scp` 之前 `destination-file` 已存在，`scp` 将覆盖该文件。

第一个示例将以 `.c` 结尾的文件从工作目录复制到本地系统 `bravo` 上的 `~jenny/archives` 目录。通配符字符没有引号，因此本地 `shell` 会对其进行扩展。由于 `archives` 是一个相对路径，`scp` 假设它是 `bravo` 上 `Jenny` 家目录的一个子目录。每个被复制的文件保留了其原始文件名。

```
$ scp *.c jenny@bravo:archives
```

接下来，`Alex` 将名为 `bravo` 的系统上 `~alex/memos` 下的目录复制到 `kudos` 上的 `~jenny/alex.memos.bravo`。他必须拥有写入 `kudos` 上 `Jenny` 家目录的必要权限。

```
$ scp -r bravo:memos jenny@kudos:alex.memos.bravo
```

最后，`Alex` 将 `Jenny` `archives` 目录中以 `.c` 结尾的文件复制到他工作目录下的 `jenny.c.bravo` 目录。通配符被引号包裹以防止被本地 `shell` 扩展；它将由远程系统 `bravo` 解析。

```
$ scp -r 'jenny@bravo:archives/*.c' jenny.c.bravo
```

需要记住，每当你复制多个文件或目录时，目标路径（无论是本地还是远程）必须是一个存在的目录，而不是一个普通文件或不存在的文件。

## sleep

创建一个休眠指定间隔的进程

`sleep time`

`sleep time-list`

`sleep` 工具使执行它的进程进入睡眠状态持续指定的时间。

### Arguments

传统上，进程睡眠的时间是以非整数参数 `time` 给出的，该时间表示秒数。然而，时间不一定是整数：你可以指定小数部分。你还可以在 `time` 后面附加单位指定：`s`（秒）、`m`（分钟）、`h`（小时）和 `d`（天）。

你可以通过在命令行中包含多个时间来构建 `time-list`：进程睡眠的总时间是这些时间的总和。例如，如果你指定了 `1h 30m 100s`，进程将睡眠 91 分钟 40 秒。

### Examples

你可以从命令行使用 `sleep` 在一段时间后执行命令。以下示例在后台运行一个进程，提醒你在 20 分钟（1,200 秒）后打电话：

```
$ sleep 1200; echo "Remember to make call." &
[1] 4668
```

或者，你可以提供以下命令来获得相同的提醒：

```
$ sleep 20m; echo "Remember to make call." &
[2] 4667
```

你还可以在 `shell` 脚本中使用 `sleep` 来每隔执行一次命令。该 `shell` 脚本每 90 秒执行一次程序更新：

```
$ cat per
#!/bin/bash
while true
do
  update
sleep 90
done
```

如果你在后台执行名为 `per` 的 `shell` 脚本，你只能通过使用 `kill` 来终止它。

最后一个 `shell` 脚本接受文件名作为参数，并等待该文件在磁盘上出现。如果文件不存在，脚本将睡眠 1 分钟 45 秒后再次检查该文件：

```
$ cat wait_for_file
#!/bin/bash

if [ $# != 1 ]; then
    echo "Usage: wait_for_file filename"
    exit 1
fi

while true
do
    if [ -f "$1" ]; then
        echo "$1 is here now"
        exit 0
    fi
    sleep 1m 45
done
```

## sort

排序和/或合并文件

`sort [options] [file-list]`

`sort` 工具用于排序和/或合并一个多个文本文件。

### Arguments

`file-list` 是包含待排序文本的一个或多个文件的路径列表。如果省略 `file-list`，`sort` 从标准输入读取。使用 `-o` 选项将其输出发送到标准输出。该工具排序并合并文件，除非你使用 `-m`（合并）或 `-c`（检查）选项。

### Options
