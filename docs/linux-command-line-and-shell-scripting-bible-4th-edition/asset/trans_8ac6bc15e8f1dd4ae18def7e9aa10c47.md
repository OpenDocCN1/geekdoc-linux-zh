

`nice` 命令会阻止普通系统用户提高其命令的优先级。请注意，尽管使用 `nice` 命令提高优先级的尝试失败了，但任务仍然会运行。只有 root 用户或具有超级用户特权的用户才能提升任务的优先级。

使用 `nice` 命令时，您不必使用 -n 选项。您可以简单地输入优先级，前面加一个连字符：

```bash
$ nice -10 ./jobcontrol.sh > jobcontrol.out &
[2] 16520
$
$ ps -p 16520 -o pid,ppid,ni,cmd
    PID  PPID  NI CMD
  16520  1630  10 /bin/bash ./jobcontrol.sh
$
```

然而，当优先级为负数时，这可能会造成混淆，因为此时需要使用双连字符。为了避免混淆，最好直接使用 -n 选项。

### 使用 renice 命令

有时，您希望更改系统上已经运行的命令的优先级。`renice` 命令在此类情况下非常有用。它允许您指定正在运行的进程的 PID 以更改其优先级：

```bash
$ ./jobcontrol.sh > jobcontrol.out &
[2] 16642
$
$ ps -p 16642 -o pid,ppid,ni,cmd
    PID  PPID  NI CMD
  16642  1630   0 /bin/bash ./jobcontrol.sh
$
$ renice -n 10 -p 16642
16642 (process ID) old priority 0, new priority 10
$
$ ps -p 16642 -o pid,ppid,ni,cmd
    PID  PPID  NI CMD
  16642  1630  10 /bin/bash ./jobcontrol.sh
$
```

`renice` 命令会自动更新正在运行的进程的调度优先级。与 `nice` 命令一样，`renice` 命令对没有超级用户特权的人有一些限制——您只能调整您拥有的进程，并且只能将其优先级降低。然而，root 用户帐户以及具有超级用户特权的用户可以使用 `renice` 命令将任何进程的优先级更改为任意值。

## 像时钟一样精准运行

当您开始处理脚本时，您可能希望在将来的某个时间运行脚本——通常是在您不在场的时候。Linux 系统提供了在预先选定的未来时间运行脚本的方法：`at` 命令、`cron` 表和 `anacron`。每种方法使用不同的技术来安排运行脚本的时间和频率。以下部分将描述这些方法中的每一种。

### 使用 at 命令调度任务

`at` 命令允许您指定一个未来的时间点，届时 Linux 系统将运行脚本。`at` 命令将任务提交到队列中，并附带有关 shell 应在何时运行该任务的说明。

`at` 守护进程 `atd` 在后台运行，并检查任务队列中是否有待运行的任务。许多 Linux 发行版在启动时自动启动此守护进程，但有些发行版甚至没有安装该软件包。如果您的发行版没有它，并且您想要安装它（第 9 章，“安装软件”），软件包名称如您可能猜测的那样，是 `at`。

`atd` 守护进程检查系统上的一个特殊目录（通常是 `/var/spool/at` 或 `/var/spool/cron/atjobs`），以查找使用 `at` 命令提交的任务。默认情况下，`atd` 守护进程每 60 秒检查一次此目录。当存在任务时，`atd` 守护进程检查任务的预定运行时间。如果时间匹配当前时间，`atd` 守护进程将运行该任务。

以下部分描述了如何使用 `at` 命令提交待运行任务以及如何管理这些任务。

### 了解 at 命令格式

基本的 `at` 命令格式相当简单：

```bash
at [-f filename] time
```

默认情况下，`at` 命令将 STDIN 的输入提交到队列。您可以使用 -f 参数指定用于读取命令（您的脚本文件）的文件名。

time 参数指定您希望 Linux 系统运行任务的时间。如果您指定了一个已经过去的时间，`at` 命令将在第二天的该时间运行任务。

在指定时间方面，您可以非常有创意。`at` 命令识别许多不同的时间格式：

- 标准的小时和分钟，如 `10:15`
- 上午/下午指示符，如 `10:15PM`
- 特定的命名时间，如 `now`、`noon`、`midnight` 或 `teatime`（`4:00 p.m.`）

除了指定运行任务的时间外，您还可以使用几种不同的日期格式包含具体日期：

- 标准日期格式，如 `MMDDYY`、`MM/DD/YY` 或 `DD.MM.YY`
- 文本日期，如 `Jul 4` 或 `Dec 25`，可以带年份也可以不带
- 时间增量：
  - `Now + 25 minutes`
  - `10:15PM tomorrow`
  - `10:15 + 7 days`

> **提示**
> 可供 `at` 工具使用的不同日期和时间格式有很多种。它们都方便地描述在 `/usr/share/doc/at/timespec` 文件中。

当您使用 `at` 命令时，任务被提交到任务队列。任务队列保存由 `at` 命令提交的处理任务。对于不同的优先级级别，共有 52 个不同的任务队列可用。任务队列使用小写字母 `a` 到 `z` 和大写字母 `A` 到 `Z` 进行引用，其中 `A` 队列与 `a` 队列是不同的队列。

**注意**

几年前，`batch` 命令是另一种允许稍后运行脚本的方法。`batch` 命令的独特之处在于，您可以安排脚本在系统使用率较低时运行。如今，`batch` 命令只是一个脚本 `/usr/bin/batch`，它调用 `at` 命令并将您的任务提交到 `b` 队列。

任务队列的字母在字母表中越靠后，任务运行的优先级越低（nice 值越高）。默认情况下，`at` 任务提交到 `a` 队列。如果您希望以较低的优先级运行任务，可以使用 -q 参数指定不同的队列字母。如果您希望与其他当前进程相比，您的任务尽可能少地消耗 CPU，最好将任务放入 `z`（小写 Z）队列。

#### 获取任务输出

当 `at` 任务在 Linux 系统上运行时，该任务没有关联的监视器。相反，Linux 系统使用提交 `at` 任务的用户的电子邮件地址作为 STDOUT 和 STDERR。任何指向 STDOUT 或 STDERR 的输出都会通过邮件系统发送给该用户。

这里有一个使用 `at` 命令在 CentOS 发行版上安排任务运行的简单示例：

```bash
$ cat tryat.sh
#!/bin/bash
# Trying out the at command
#
echo "This script ran at $(date +%B%d,%T)"
echo
echo "This script is using the $SHELL shell."
echo
sleep 5
echo "This is the script's end."
#
exit
$
$ at -f tryat.sh now
warning: commands will be executed using /bin/sh
job 3 at Thu Jun 18 16:23:00 2020
$
```

`at` 命令显示分配给任务的编号以及计划运行任务的时间。-f 选项指定使用的脚本文件，而 `now` 时间指示符指示 `at` 立即运行脚本。

**注意**

不要让 `at` 命令发出的那个警告消息让您担心。由于此脚本的第一行是 `#!/bin/bash`，此 shell 脚本中的命令将由 Bash shell 执行。

使用电子邮件作为 `at` 命令的输出最多也只是不方便。`at` 命令通过 `sendmail` 应用程序发送电子邮件。如果系统不使用 `sendmail`，您将不会收到任何输出！因此，使用 `at` 命令时，最好在脚本中重定向 STDOUT 和 STDERR（第 15 章），如以下示例所示：

```bash
$ cat tryout.sh
#!/bin/bash
# Trying out the at command redirecting output
#
outfile=$HOME/scripts/tryat.out
#
echo "This script ran at $(date +%B%d,%T)" > $outfile
echo >> $outfile
echo "This script is using the $SHELL shell." >> $outfile
echo >> $outfile
sleep 5
echo "This is the script's end." >> $outfile
#
exit
$
$ at -M -f tryatout.sh now
warning: commands will be executed using /bin/sh
job 4 at Thu Jun 18 16:48:00 2020
$
$ cat $HOME/scripts/tryat.out
This script ran at June18,16:48:21
This script is using the /bin/bash shell.
This is the script's end.
$
```

如果您不想在使用 `at` 时使用电子邮件或重定向，最好添加 -M 选项以抑制由使用 `at` 命令的作业生成的任何输出。

### 列出待处理任务

`atq` 命令允许您查看系统上待处理的任务：

```bash
$ at -M -f tryatout.sh teatime
warning: commands will be executed using /bin/sh
job 5 at Fri Jun 19 16:00:00 2020
$
$ at -M -f tryatout.sh tomorrow
warning: commands will be executed using /bin/sh
job 6 at Fri Jun 19 16:53:00 2020
$
$ at -M -f tryatout.sh 20:30
warning: commands will be executed using /bin/sh
job 7 at Thu Jun 18 20:30:00 2020
$
$ at -M -f tryatout.sh now+1hour
warning: commands will be executed using /bin/sh
job 8 at Thu Jun 18 17:54:00 2020
$
$ atq
      Thu Jun 18 16:11:00 2020 a  christine
      Fri Jun 19 16:00:00 2020 a  christine
```

