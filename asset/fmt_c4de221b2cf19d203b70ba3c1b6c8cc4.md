
## 1. 查看进程信息

```
root 467 433 0 18:12 tty 00:00:00 sh /usr/X11R6/bin/start
root 474 467 0 18:12 tty 00:00:00 xinit /etc/X11/xinit
root 478 474 0 18:12 tty 00:00:00 /usr/bin/gnome-session
root 487 1 0 18:12 tty 00:00:00 gnome-promptry --sm-client-id
root 503 1 0 18:12 tty 00:00:00 [enlightenment]
root 506 1 0 18:12 tty 00:00:00 -sm-client-id defaults
root 508 1 0 18:12 tty 00:00:00 xcreensaver -no-splash -timeout
root 510 1 0 18:12 tty 00:00:01 gmc --sm-client-id default0
root 512 1 0 18:12 tty 00:00:01 gnome-help-browser --sm-client-i
root 649 445 0 18:22 tty 00:00:00 su
root 653 669 0 18:24 tty 00:00:00 bash
neil 655 428 1 28:24 tty 00:00:00 terminal
root 715 713 1 18:28 tty 00:00:00 gnome-pty-helper
root 717 716 13 18:28 pts/0 00:00:01 emacs
root 718 653 0 18:22 tty 00:00:00 ps -af
```

这显示了许多进程的信息

```
UID PID PPID C STIME TTY TIME CMD
root 433 425 0 18:12 tty1 00:00:00 [bash]
rick 445 426 0 18:12 tty2 00:00:00 -bash
rick 456 427 0 18:12 tty3 00:00:00 [bash]
```

执行命令 `ps -af`

```
UID PID PPID C STIME TTY TIME CMD
root 433 425 0 18:12 tty1 00:00:00 [bash]
rick 445 426 0 18:12 tty2 00:00:00 -bash
rick 456 427 0 18:12 tty3 00:00:00 [bash]
```

## 2. 执行命令 ps -af

```
root 467 433 0 18:12 tty 00:00:00 sh /usr/X11R6/bin/start
root 474 467 0 18:12 tty 00:00:00 xinit /etc/X11/xinit
root 478 474 0 18:12 tty 00:00:00 /usr/bin/gnome-session
root 487 1 0 18:12 tty 00:00:00 gnome-promptry --sm-client-id
root 503 1 0 18:12 tty 00:00:00 [enlightenment]
root 506 1 0 18:12 tty 00:00:00 -sm-client-id defaults
root 508 1 0 18:12 tty 00:00:00 xcreensaver -no-splash -timeout
root 510 1 0 18:12 tty 00:00:01 gmc --sm-client-id default0
root 512 1 0 18:12 tty 00:00:01 gnome-help-browser --sm-client-i
root 649 445 0 18:22 tty 00:00:00 su
root 653 669 0 18:24 tty 00:00:00 bash
neil 655 428 1 28:24 tty 00:00:00 terminal
root 715 713 1 18:28 tty 00:00:00 gnome-pty-helper
root 717 716 13 18:28 pts/0 00:00:01 emacs
root 718 653 0 18:22 tty 00:00:00 ps -af
```

这显示了许多进程的信息

```
UID PID PPID C STIME TTY TIME CMD
root 433 425 0 18:12 tty1 00:00:00 [bash]
rick 445 426 0 18:12 tty2 00:00:00 -bash
rick 456 427 0 18:12 tty3 00:00:00 [bash]
```

执行命令 `ps -af`

```
UID PID PPID C STIME TTY TIME CMD
root 433 425 0 18:12 tty1 00:00:00 [bash]
rick 445 426 0 18:12 tty2 00:00:00 -bash
rick 456 427 0 18:12 tty3 00:00:00 [bash]
```

## 3. 命令说明

`ps` 命令显示我们正在运行的进程，另一个用户正在运行的进程，或者系统上所有的进程。以下是示例输出：

`ps` 的显示输出包含用户正在运行的进程，或者用户显示的、运行的进程信息。

```
root 467 433 0 18:12 tty 00:00:00 sh /usr/X11R6/bin/start
root 474 467 0 18:12 tty 00:00:00 xinit /etc/X11/xinit
root 478 474 0 18:12 tty 00:00:00 /usr/bin/gnome-session
root 487 1 0 18:12 tty 00:00:00 gnome-promptry --sm-client-id
root 503 1 0 18:12 tty 00:00:00 [enlightenment]
root 506 1 0 18:12 tty 00:00:00 -sm-client-id defaults
root 508 1 0 18:12 tty 00:00:00 xcreensaver -no-splash -timeout
root 510 1 0 18:12 tty 00:00:01 gmc --sm-client-id default0
root 512 1 0 18:12 tty 00:00:01 gnome-help-browser --sm-client-i
root 649 445 0 18:22 tty 00:00:00 su
root 653 669 0 18:24 tty 00:00:00 bash
neil 655 428 1 28:24 tty 00:00:00 terminal
root 715 713 1 18:28 tty 00:00:00 gnome-pty-helper
root 717 716 13 18:28 pts/0 00:00:01 emacs
root 718 653 0 18:22 tty 00:00:00 ps -af
```

这显示了许多进程的信息，以及涉及 `emacs` 编辑器的进程。

`ps` 命令显示我们正在运行的进程，另一个用户正在运行的进程，或者系统上所有的进程。以下是示例输出：

执行命令 `ps -af`

```
UID PID PPID C STIME TTY TIME CMD
root 433 425 0 18:12 tty1 00:00:00 [bash]
rick 445 426 0 18:12 tty2 00:00:00 -bash
rick 456 427 0 18:12 tty3 00:00:00 [bash]
```
