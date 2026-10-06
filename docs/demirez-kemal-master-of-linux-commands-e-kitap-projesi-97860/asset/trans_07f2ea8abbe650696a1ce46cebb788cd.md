

# Linux 命令精解

## Tail

重要的文件之一是 messages 文件。许多系统事件的记录都在这个文件中。要查看实时写入 messages 文件的记录，你可以使用 `tail -f /var/log/messages` 命令。

```
root@kemma:~# tail -f /var/log/messages
Nov 22 23:59:44 kemma gnome-session(828): myAppIcon.onChanged()/usr/share/
gnome-shell/extensions/dash-to-dock@micxr.gmail.com/my.Desh.js:1354
Nov 22 23:59:44 kemma gnome-session(828): wrapper@resource:///org/gnome/js/modules/utils.js:100
Nov 22 23:59:57 kemma gnome-session(828): (gnome-shell:923): mutter-WARNING *
STACK OP RAISE ABOVE: window 0x5b014001a not in stack
Nov 22 23:59:57 kemma gnome-session(828): (gnome-shell:923): mutter-WARNING **
STACK OP RAISE ABOVE: window 0x5b014001a not in stack
Nov 22 23:59:57 kemma gnome-session(828): (gnome-shell:923): mutter-WARNING *
STACK OP RAISE ABOVE: window 0x5b014001a not in stack
```

## Dmesg

系统向内核发送信息。这些信息被写入内核日志缓冲区中。要查看这些内核日志消息，我们使用 `dmesg`。

```
root@kemma:~# dmesg
000000 Initializing cgroup subsystems cgroup
000000 Initializing cgroup subsystems cpuset
000000 Initializing cgroup subsystems cpuacct
000000 Linux version 4.4.0-111-x86 (debian-kernel-lists@debian.org)
(gcc version 4.9.3-10ubuntu1) (gcc 4.9.0) SMP 4.4.0-111+li2 (2015-06-03)

000000 Disabled fast startup probe
000000 BIOS-e820: mem 0x0000000000000000-0x00000000ffffffff usable
000000 BIOS-e820: mem 0x0000000100000000-0x00000001ffffffff reserved
000000 BIOS-e820: mem 0x0000000200000000-0x00000002ffffffff reserved
000000 BIOS-e820: mem 0x0000000300000000-0x00000003ffffffff usable
```

当然，如果你想根据任何标准列出内核消息，可以使用 `dmesg`。例如 `dmesg | grep fail`。你也可以使用 `dmesg -c` 来删除内核日志记录。

```
root@kemal:~# dmesg -c
root@kemal:~# dmesg
root@kemal:~# _
```

## Last

要列出系统中最后登录会话的用户，可以使用 `last` 命令。

```
root@kemal:~# last
root pts/0          :0 Mon Nov 23 00:01 still logged in
root pts/1          :0 Sun Nov 22 21:49 - 00:03 (02:14)
root pts/0          :0 Sun Nov 22 20:58 - 22:09 (01:11)
root pts/0          :0 Sun Nov 22 20:57 - 20:58 (00:01)
root pts/1          :0 Sun Nov 22 18:26 - 20:58 (02:31)
root                 :0 Sun Nov 22 18:24 still logged in
(unknown)            :0 Sun Nov 22 18:23 - 18:23 (00:00)
reboot system boot  4.0.0-kalil-686- Sun Nov 22 18:23 - 00:19 (05:56)
root pts/0          :0 Sun Nov 22 12:09 - 12:10 (00:00)
```

例如，你想查看最后 3 次登录系统的用户列表，可以使用 `-3` 命令：

```
root@kemal:~# last -3
root pts/0          :0
root pts/1          :0
root pts/0          :0
```

wtmp begins Sun Nov 22 11:07:09 2015

要查看任何用户的最后登录信息，可以使用 `last <user_name>`。

## Btmp

错误日志文件条目保存在 `btmp` 文件中。由于这是一个数据文件，我们可以使用 `strings btmp` 命令来获取文件中内容的打印列表。

![](img/aa6ce54dbb8ffe5b9d7befb8c6764064_276_0.png)

```
root@kemal:/var/log# file btmp
btmp: dBase III DBT, version number 0, next free block index 7
root@kemal:/var/log# strings btmp
root
uuARVeY
guest
root@kemal:/var/log# _
```

## Lastlog

要查看用户打开会话时的地址，可以使用 `lastlog` 命令。当然，这些用户可能是使用系统服务的人。它显示了运行服务的用户信息和地址信息。对于任何用户的信息，可以使用 `lastlog <user_name>`。

## Utmp

`utmp` 文件包含当前登录系统的用户信息。要查看这些信息，我们可以使用 `last` 命令。

```
root@kemal:~# last
```

`wtmp` 文件包含过去登录用户信息。要查看这些信息，我们可以使用 `last` 命令。

`btmp` 文件包含失败登录尝试的信息。要查看这些信息，我们可以使用 `last -f` 命令。

`lastlog` 文件包含每个用户最后登录的时间。要查看这些信息，我们可以使用 `lastlog` 命令。

