
要在计划时间运行命令，或者在未与你的 shell 会话绑定的情况下运行，可以使用 `at` 和 `batch` 命令。要在固定时间重复运行命令，有 `cron` 和 `anacron` 机制。你也可以将脚本（或脚本的符号链接）放入 `/etc/cron.hourly`（或 `cron.daily`、`cron.weekly` 或 `cron.monthly`）。

# 第 9 章：检查和管理运行中的进程

## 本章内容

- 使用 `ps` 和 `top` 查看活动进程
- 使用 `pgrep` 搜索进程
- 使用 `nice` 和 `renice` 调整 CPU 优先级
- 将进程移动到后台 `bg` 或前台 `fg`
- 使用 `kill` 和 `killall` 杀死并向进程发送信号
- 使用 `at` 和 `batch` 命令
- 使用 `cron` 调度重复运行命令

## 列出活动进程

要查看系统当前正在运行哪些进程，大多数人使用 `ps` 和 `top` 命令。`ps` 命令提供了当前运行进程的快照（以简单列表形式）。`top` 命令提供了一个面向屏幕的持续更新的运行命令列表，并根据你的选择进行排序（如 CPU 使用率、内存使用率、UID 等）。

## 使用 ps 查看活动进程

每个 Linux 系统（以及 Unix、BSD、Mac OS 等其他系统）都包含了 `ps` 命令。多年来，`ps` 出现了许多略不同的版本，提供了不同的选项（例如，允许你在 SUSE、openSUSE 和大多数 Linux 系统中使用 `-`）。本章展示了关于如何显示当前用户运行进程的一些示例。表 9-1 列出了列的描述：

```
$ ps                          显示当前用户的进程
PID TTY                       COMMAND
2552 pts/0                   00:00:00 bash
3438 pts/0                   00:00:00 ps
$ ps -u chris                 显示 chris 的进程（简单输出）
PID TTY                       COMMAND
2678 tty 1                  00:00:00 startx
2689 tty 1                  00:00:00 xinit
2710 tty 1                  00:00:00 gnome-session
$ ps -u chris                 显示 chris 的进程（带 CPU/MEM）
USER      PID %CPU %MEM VZ RSS TTY     STAT START CMD
chris     2678 2645 0.00 428 852 tty S+  Aug25 00:00:00 /bin/sh
chris     2689 2678 0.01 240 888 tty S+  Aug25 00:00:00 xinit
chris     2710 2710 0.01 2216 5496 tty S  Aug25 00:06:00 /usr/bin/gnome-session
$ ps -Fu chris                 显示 chris 的进程（带 SZ 和 PR）
USER      PID %CPU %MEM VZ RSS TTY     STAT START CMD
chris     2678 2645 0.00 1082 852 tty S+  Aug25 00:00:00 /bin/sh startx
chris     2689 2678 0.00 602 888 tty S+  Aug25 00:00:00 xinit
chris     2710 2689 0.00 5550 5440 tty S  Aug25 00:00:09 gnome-session
```

这些示例说明了运行 GNOME 桌面会话的用户进程外观。第一个示例显示了从终端窗口运行的进程，你只能看到在该窗口中运行的当前 shell。其他示例允许为每个进程显示不同的信息（产生自定义输出的方法见后文示例）。表 9-1 用于显示的列的描述。

以下是显示系统中运行的所有进程的 `ps` 示例：

```
$ ps -e
显示所有运行进程
PID TID CMD
1 ?       00:00:01 init
2 ?       00:00:00 migration/0
3 ?       00:00:00 ksoftirqd/0
$ ps -el
显示所有运行进程，长列表
F S PPID C NI ADDR SZ TTY TIME CMD
4 S 0 1 0 75 534 - ? 00:00:01
1 S 0 2 1 - - ? 00:00:00 migration/0
3 S 0 1 0 94 - ? 00:00:00 ksoftirqd/0
$ ps -ef
显示所有运行进程，完整列表
UID PPID C SZ RSS TTY TIME CMD
root 1 0 Aug25? 00:00:01 [5]
root 2 1 0 Aug25? 00:00:00 migration/0
root 3 1 0 Aug25? 00:00:00 ksoftirqd/0
$ ps ax
显示所有运行进程，短格式
PID TID STAT TIME
1 ? S 0:01 [5]
2 ? S 0:00 [migration/0]
3 ? S 0:00 [ksoftirqd/0]
$ ps aux
显示所有运行进程，长 BSD 格式
USER      PID %CPU %MEM VSZ RSS TTY STAT TIME CMD
root 1 0.0 2136 556 ? S Aug25 01:01 [5]
root 2 0.0 0 ? S Aug25 00:00 [migration/0]
root 3 0.0 0 ? S Aug25 00:00 [ksoftirqd/0]
$ ps auwx
显示所有运行进程，长 BSD 格式，无限宽度
```

某些进程会启动其他进程。例如，Web 服务器 `httpd` 会派生多个守护进程来处理你 Web 服务器的请求。你可以使用选项查看进程的层次结构（树形）：

```
$ ps -ejH

显示带进程/会话 ID 的进程层次结构

PID PGID TID COMMAND

1 1 1 ? 00:00:01 init

2 1 2 ? 00:00:00 migration/0

3 1 3 ? 00:00:00 ksoftirqd/0
```
