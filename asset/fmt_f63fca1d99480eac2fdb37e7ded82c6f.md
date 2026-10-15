
| UID | PID | PPID | C | TTY | CMD |
|---|---|---|---|---|---|
| root | 1 | 0 | 0 | ? | 00:00:00 | `/usr/lib/systemd/systemd` |
| root | 2 | 0 | 0 | ? | 00:00:00 | `[softirqd]` |
| root | 3 | 0 | 0 | ? | 00:00:00 | `[kworker/0]` |
| root | 5 | 0 | 0 | ? | 00:00:00 | `[kworker/u8:0]` |
| root | 6 | 0 | 0 | ? | 00:00:00 | `[migration/0]` |
| root | 7 | 0 | 0 | ? | 00:00:00 | `[rcu-bh]` |
| root | 8 | 0 | 0 | ? | 00:00:00 | `[rcu-sched]` |
| root | 9 | 2 | 0 | ? | 00:00:00 | `[watchdog/0]` |
| root | 10 | 2 | 0 | ? | 00:00:00 | `[helper]` |
| root | 11 | 2 | 0 | ? | 00:00:00 | `[devfs]` |
| root | 12 | 2 | 0 | ? | 00:00:00 | `[netns]` |
| root | 13 | 2 | 0 | ? | 00:00:00 | `[writeback]` |
| root | 14 | 2 | 0 | ? | 00:00:00 | `/sbin/auditd` |
| root | 394 | 1 | 0 | ? | 00:00:00 | `/sbin/audisp` |
| root | 407 | 394 | 0 | ? | 00:00:00 | `/usr/sbin/dispatch` |
| root | 409 | 407 | 0 | ? | 00:00:00 | `/usr/sbin/alsactl -n` |
| root | 411 | 1 | 0 | ? | 00:00:00 | `/sbin/rngd -f` |
| root | 418 | 1 | 0 | ? | 00:00:00 | `/sbin/ModemManager` |
| root | 420 | 1 | 0 | ? | 00:00:00 | `avahi-daemon: running` |
| avahi | 422 | 1 | 0 | ? | 00:00:00 | `/bin/dbus-daemon --system` |
| dbus | 424 | 1 | 0 | ? | 00:00:00 | `/usr/sbin/chronyd -u` |
| chrony | 430 | 1 | 0 | ? | 00:00:00 | `/usr/sbin/crond -f` |
| root | 431 | 1 | 0 | ? | 00:00:00 | `/usr/sbin/atd -s` |
| root | 432 | 1 | 0 | ? | 00:00:00 | `/usr/sbin/abtrd` |
| root | 435 | 1 | 0 | ? | 00:00:00 | `/usr/sbin/abrt-watch-log` |
| root | 437 | 1 | 0 | ? | 00:00:00 | `/usr/sbin/gdm` |
| root | 441 | 1 | 0 | ? | 00:00:00 | `/usr/sbin/mcelog` |
| root | 446 | 1 | 0 | ? | 00:00:00 | `/usr/sbin/libexec/gdm-simple` |
| root | 481 | 1 | 0 | ? | 00:00:00 | `/usr/lib/polkit-1/polkit` |
| polkit | 482 | 1 | 0 | ? | 00:00:00 | `/usr/bin/Xorg :0` |
| root | 488 | 1 | 0 | tty1 | 00:00:00 | `gdm-session-worker` |
| root | 551 | 481 | 0 | ? | 00:00:00 | `/usr/sbin/NetworkManager` |
| root | 552 | 1 | 0 | ? | 00:00:00 | `(sd-pam)` |
| gdm | 842 | 823 | 0 | ? | 00:00:00 | `/usr/bin/gnome-session` |
| gdm | 852 | 551 | 0 | ? | 00:00:00 | `/usr/bin/dbus-launch` |
| gdm | 856 | 1 | 0 | ? | 00:00:00 | `/bin/dbus-daemon --fork` |
| gdm | 1018 | 1 | 0 | ? | 00:00:00 | `/sbin/dhclient -d -sf` |

# 第 9 章 管理 Linux 进程

| PID | PPID | CIME | TTY | TIME | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- |
| gdm | 1025 | 1 | 01:23 | ? | 00:00:00 | `/usr/libexec/at-spi-bus` |
| gdm | 1045 | 1025 | 01:23 | ? | 00:00:00 | `/bin/dbus-daemon` |
| root | 1072 | 1 | 01:23 | ? | 00:00:00 | `/usr/libexec/upowered` |
| gdm | 1077 | 852 | 01:23 | ? | 00:00:03 | `gnome-shell --gdm` |
| colord | 1080 | 1 | 01:23 | ? | 00:00:00 | `/usr/libexec/colorord` |
| gdm | 1087 | 1 | 01:23 | ? | 00:00:00 | `/usr/bin/pulseaudio` |
| gdm | 1114 | 1 | 01:23 | ? | 00:00:00 | `/usr/libexec/ibus-dconf` |
| gdm | 1122 | 1 | 01:23 | ? | 00:00:00 | `/usr/libexec/ibus-engine` |
| gdm | 1148 | 1 | 01:23 | ? | 00:00:00 | `/usr/libexec/go-daemon` |
| root | 1164 | 1 | 01:23 | ? | 00:00:00 | `login - root` |
| root | 1174 | 1171 | 01:23 | ? | 00:00:00 | `(sd-pam)` |
| root | 1175 | 1164 | 01:23 | tty2 | 00:00:00 | `-bash` |
| root | 1208 | 2 | 01:28 | ? | 00:00:00 | `[kworker/0]` |
| root | 1213 | 1 | 01:23 | ? | 00:00:00 | `/usr/sbin/sshd -D` |
| root | 1216 | 1213 | 01:23 | ? | 00:00:00 | `sshd:root@pts/0` |
| root | 1220 | 1216 | 01:23 | pts/0 | 00:00:00 | `-bash` |
| root | 1253 | 2 | 01:23 | ? | 00:00:00 | `[kworker/0:2]` |
| root | 1260 | 1 | 01:23 | ? | 00:00:00 | `/usr/libexec/packagekit` |
| root | 1742 | 1220 | 01:23 | pts/0 | 00:00:00 | `ps -ef` |

如前面的输出所示，内核守护进程（kthread）的 PID 为 2，并启动了实际 Linux 内核中的大多数子进程，因为子进程的 PPID 为 2；而 init 守护进程（`/usr/lib/systemd/system`, PID = 1）启动了其他守护进程，因为这些守护进程的 PPID 为 1。此外，守护进程和内核子进程的 TTY 列中显示为 `?`，因为它们并不在终端上运行。

由于在 Linux 服务器上，`ps -ef` 命令的输出可能达几百行，因此你通常会将其输出管道到 `less` 命令，以逐页将输出发送到终端页面，或者管道到 `grep` 命令，后者用于显示仅包含相关信息的行。例如，要仅显示系统上的 BASH shell，你可以使用以下命令：

```
[root@server1 ~]# ps -ef | grep bash

user    2094    2008 0 14:29/pts/1 00:00:00 -bash

root    2159    2156 0 14:30/tty2 00:00:00 -bash
```
