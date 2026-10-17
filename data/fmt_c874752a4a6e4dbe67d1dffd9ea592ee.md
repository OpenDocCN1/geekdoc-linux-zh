
- 僵尸进程和孤进程长时间存在会消耗系统资源，应该被杀死以提高系统性能。

- 你可以使用 `kill`、`killall` 和 `top` 命令向进程发送杀死信号。

- BASH 会为派生（forks）创建一个子 shell 来执行大多数命令。

## 关键术语

- 进程可以在后台运行，并可以使用命令名指定。BASH shell 会为每个后台进程分配一个后台作业 ID（job ID），以便之后对其进行操作。

- 进程的优先级可以通过更改其值来间接影响；值范围从 -20（高优先级）到 +19（低优先级）。只有 `root` 用户可以增加进程的优先级。

- 你可以使用 `at` 和 `cron` 守护进程调度命令在以后运行。`at` 守护进程调度任务在未来的某个时间点发生，而 `cron` 守护进程则使用 cron 表调度任务在未来重复性地执行。

## 关键术语

- `etc/at.allow` 列出所有可以使用 `at` 命令的用户的文件。

- `etc/at.deny` 列出所有无法访问 `at` 命令的用户的文件。

- `etc/cron.allow` 一个列出所有可以使用 `cron` 命令的用户的文件。

- `etc/cron.d` 包含额外系统 cron 表的目录。

- `etc/cron.deny` 一个列出所有无法访问 `cron` 命令的用户的文件。

- `etc/crontab` 默认系统 cron 表。

- `var/spool/at` 存储用于通过守护进程调度命令的信息的目录。

- `var/spool/cron` 存储 cron 表的目录。

- `at` 用于调度命令和任务在未来预设时间运行的命令。

- `at (atd)` 在未来时间执行任务的系统守护进程；它通过 `at` 命令进行配置。

- `background (bg)` 用于将前台进程在后台运行的命令。

- **后台进程 (background process)** 不需要 BASH shell 等待其终止的进程。执行后，用户会立即收到 BASH 提示符。

- **子进程 (child process)** 由另一个进程（父进程）启动的进程。

- **cron 守护进程 (crond)** 在未来重复执行任务的系统守护进程，并使用 `cron` 进行配置。

- `crontab` 用于查看和编辑 cron 表的命令。

- **cron 表 (cron table)** 指定由 cron 守护进程执行的任务的文件；分为用户 cron 表和系统 cron 表。

- **守护进程 (daemon process)** 不与终端关联的进程。

- `foreground (fg)` 用于将后台进程在前台运行的命令。

- **前台进程 (foreground process)** BASH shell 必须等待其终止的进程。

- **派生 (forking)** 从父 BASH shell 创建新的 BASH shell 进程的行为。

- `jobs (jobs)` 用于查看当前 shell 中运行的后台进程列表的命令。

![](img/bafa5678973f896b93838a140b8f7840_444_0.png)

# 第 9 章 管理 Linux 进程

- `killall` 命令 按名称杀死所有进程实例的命令。

- `kill` 命令 用于杀死或终止进程的命令。

- **kill 信号 (kill signal)** `kill` 命令发送给进程的信号类型；不同的 kill 信号会以不同的方式影响进程。

- `nice` 命令 用于在进程启动时更改其优先级的命令。

- **nice 值 (nice value)** 间接反映进程优先级的值；值越高，优先级越低。

- **父进程 (parent process)** 已经启动了其他进程（子进程）的进程。

- **父进程 ID (PPID)** 创建该进程的父进程的 PID。

- **进程 (process)** 当前加载到物理内存并在系统上运行的程序。

- **进程 ID (PID)** 在每个进程开始时被分配的唯一标识符。

- **进程优先级 (process priority)** 分配给进程的数字，用于确定处理器将获得多少次时间片；越高，优先级越低。

- **进程状态 (process state)** 进程的当前状态；大多数进程处于 nsleep（休眠）或 running（运行）状态。

- **程序 (program)** 存储在文件系统中可执行文件中的结构化命令集。可以执行一个程序来运行一个进程。

- `ps` 命令 用于获取系统上当前运行进程信息的命令。

- `pstree` 命令 根据进程的谱系（从 init 守护进程开始）显示进程的命令。

- `renice` 命令 用于修改系统中当前运行进程的 nice 值的命令。

- **流氓进程 (rogue process)** 以某种方式出现故障，并持续消耗远超其所需的资源的进程。

- **时间片 (time slice)** 在多处理系统中给予进程的 CPU 时间。

- `top` 命令 用于获取系统上最活跃进程的实时信息的命令；它也可以用于 `renice` 或 `kill` 进程。

- **捕获 (trapping)** 忽略 kill 信号的过程。

- **用户进程 (user process)** 由用户启动并在终端上运行的进程。

- **僵尸进程 (zombie process)** 已完成执行但其父进程尚未释放其 PID 的进程；僵尸进程在内核进程表中保留一个位置。

## 复习题

1. 不带参数输入的哪种命令用于显示在当前 shell 中运行的进程列表？
    a. `ppid`
    b. `list`
    c. `pid`
    d. `ps`

2. 下列哪个说法是正确的？（多选）
    a. 如果 `/etc/allow` 存在，只有列在其中的用户才能使用 `cron` 命令。
    b. 如果 `/etc/cron.allow` 存在，只有列在其中的用户可以使用 `cron` 命令。
    c. 如果 `/etc/cron.deny` 拒绝且 `/etc/cron.allow` 不存在，任何用户都可以使用 `cron` 命令。
    d. 如果 `/etc/cron.allow` 和 `/etc/cron.deny` 存在，只有列在前者中的用户可以使用 `cron` 命令，列在后者中的用户被拒绝。
    e. 如果 `/etc/cron.allow` 存在，只有列在其中的用户可以使用 `cron` 命令。

3. 使用 cron 调度运行的单个任务存储在哪里？
    a. `crontab`
    b. `cron`
    c. `var/spool/cron`
    d. `var/spool/at`

4. 哪个进程的 PID 始终为 1？
    a. 内核
    b. `ps`
    c. `init`
    d. `top`

5. 进程派生或启动另一个进程被称为
    a. child process
    b. forking
    c. branching
    d. parenting

6. 由于守护进程不与终端关联，你必须使用 `ps` 的 `-e` 切换来查看它们。对或错？

7. 下列哪种命令最可能增加进程获得时间片的概率？
    a. `renice 0`
    b. `renice 15`
    c. `renice -12`
    d. `renice 19`

8. 你如何跳过等待函数并将用户进程发送到后台？
    a. 进程一旦执行就无法发生这种情况；只能通过在后面加上取符符号 (`&`) 来完成。
    b. 这种情况不会；只有守护进程可以在后台运行。
    c. 你可以使用 `ps` 命令。
    d. 你可以使用 `Ctrl+z` 键和 `fg` 命令。

9. `at` 命令用于
    a. 调度进程在后台定期运行
    b. 调度进程在未来周期性地循环运行
    c. 调度进程在未来的某个单实例运行
    d. 调度进程在前台运行

10. 使用哪种命令查看和修改通过 cron 调度运行的用户作业（user jobs）？
    a. `crontab`
    b. `cron`
    c. `ps`
    d. `sched`

11. 每个进程都有一个进程 ID 和一个
    a. fork process
    b. daemon
    c. child process
    d. parent process ID

12. `killall` 命令终止了
    a. 所有具有相同 `PPID` 的进程实例
    b. 所有具有相同 `PID` 的进程实例
    c. 所有具有相同优先级的进程实例
    d. 所有具有相同名称的进程实例

13. Nice 值用于通过以下范围影响进程优先级
    a. 0 和 20
    b. 0 和 -19
    c. -19 和 20
    d. -20 和 19

14. 不与终端关联的进程名称是什么？
    a. child process
    b. parent process
    c. user process
    d. daemon process

15. 要杀死后台运行的进程，你必须在其进程 ID 之前放置一个 `%` 字符。正确或错误？

16. 哪种 kill 信号不能被捕获（trap）？
    +   a. 1
    b. 9
    c. 3
