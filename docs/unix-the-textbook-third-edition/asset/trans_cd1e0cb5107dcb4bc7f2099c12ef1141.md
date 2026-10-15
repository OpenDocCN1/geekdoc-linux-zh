

```
$ nohup find / -name foo -print 1> foo.paths 2> /dev/null &
[1] 62808
$ kill -1 62808
$ jobs
[1]+ Running  nohup find / -name foo -print > foo.paths 2> /dev/null &
$ kill 62808
$ <Enter>
[1]+ Terminated  nohup find / -name foo -print > foo.paths 2> /dev/null
$ jobs
$
```

如果用分号分隔命令，你可以用 nohup 运行它们。在下面的会话中，GenData 生成一些数据并将其放入名为 employees 的文件中，而 sort 命令对文件进行排序并将排序后的版本存储在 employees.sorted 文件中。

```
$ nohup GenData > employees ; sort employees > employees.sorted &
[2] 15931
$
```

在下面的本章练习中，你将使用 kill 命令练习异常终止进程，并使用 nohup 和 ps -a 命令体会如何在注销时仍能运行不会终止的进程。

## EXERCISE 10.7

给出一个用于终止 PID 为 10974 且 jobID 为 3 的进程的命令。

## EXERCISE 10.8

运行第一个 nohup 命令，使用 ps 验证命令正在执行，注销，再次登录，并使用 ps -a 命令确定 find 命令是否仍在运行。

## 10.7 PROCESS HIERARCHY IN UNIX

当你打开 UNIX 系统时，内核在执行一些检查和其他日常任务后，会从头创建第一个进程。在 PC-BSD 中，该进程称为 kernel，在 Solaris 中称为 sched。该进程没有父进程，其 PID 为 0。该进程的 PPID 也为 0。然后它会生成多个其他进程，这些进程旨在处理多个重要的内核任务，包括与虚拟内存、文件处理、中断处理相关的任务，以及在启动时执行各种任务，例如

初始化硬件端口。表 10.12 给出了其中一些进程及其用途的列表。

### TABLE 10.12 Some of the Key Processes Created by kernel (on PC-BSD) and sched (on Solaris)

| PC-BSD | Solaris | Purpose |
|---|---|---|
| init | init | Granddaddy of all user processes; all user-level services, including all Internet services, and user processes run under the children of this process. |
| pagedaemon | pageout | Read/write pages from/to disk |
| bufdaemon | fsflush | Supplies clean pages/buffers by writing dirty pages/buffers to disk |
| zfskern | zpool-rpool | Performs I/O tasks related to ZFS pools |
| intr | intrd | Handles all interrupts (lower-half of the kernel) |
| vmdaemon | vmtasks | Moves processes from main memory to disk storage |

init 进程是所有创建的用户进程的鼻祖，只要系统处于运行状态。init 进程的 PID 为 1，并以超级用户权限运行。该进程的可执行二进制文件位于 PC-BSD 下的 /sbin/init 文件中，在 Solaris 下位于 /usr/sbin/init。该进程在执行 /etc/rc 文件中给出的多个活动后，读取 /etc/ttys 文件以确定哪些 I/O（终端）线路应处于活动状态。对于每条活动线路，init 从 /etc/getty 启动一个 getty 进程。getty 进程也以超级用户模式运行，根据 /etc/termcap 文件中指定的设置终端属性，例如波特率。然后它显示 login: 提示符，邀请你登录到终端。

在 login: 提示符下，当你输入登录名并按下 <Return> 时，getty 进程会派生一个子进程。子进程执行 exec 系统调用，以你的登录名为参数成为登录进程。登录进程提示你输入密码并检查你的登录名和密码的有效性。如果它发现两者都正确，登录进程会 exec 成为你的登录 shell。如果登录进程在 /etc/passwd 文件中找不到你的登录名或发现你输入的密码与 /etc/passwd 文件中的密码不匹配，它会显示错误消息并终止。控制权返回到 getty 进程，后者重新显示 login: 提示符。一旦进入你的登录 shell，你可以进行工作并通过按下 <Ctrl+D> 或运行 exit 命令终止 shell。 当你这样做时，shell 进程终止，控制权返回到 getty 进程，后者显示 login: 提示符，生活继续。

当你通过 ssh 命令登录时，远程机器上的 sshd 守护进程（Secure Shell 服务器进程）会为你创建一个子 sshd 进程（你的私有 sshd），该进程处理与你的客户端的通信。服务器 sshd 返回去寻找来自其他客户端的更多 SSH 连接请求。你的私有 sshd 再生成另一个 sshd 进程，该进程用伪终端 pts/1 覆盖自身，提示你输入密码。当你输入正确的密码后，它会为你运行登录 shell 进程。默认情况下，登录 shell 在 PC-BSD 上为 C shell，在 Solaris 上为 Bash。你在你的

