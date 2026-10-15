
你应该能看到一个进程列表。

| PID | TTY | STAT | COMMAND |
|---|---|---|---|
| 1 ? | S | 0:04 init [5] |
| 2 ? | SW | 0:00 [kflushd] |
| 3 ? | SW | 0:00 [kpiod] |
| 4 ? | SW | 0:00 [kswapd] |
| 5 ? | SW | 0:00 [mdrecovery] |
| 260 ? | S | 0:00 ypserv |
| 275 ? | SW | 0:00 [ypbind] |
| 280 ? | S | 0:00 ypbind (slave) |
| 306 ? | S | 0:00 syslog -m 0 |
| 317 ? | S | 0:00 klogd |
| 345 ? | S | 0:00 crond |
| 359 ? | S | 0:00 inetd |
| 366 ? | SW | 0:00 [sshd2] |
| 380 ? | S | 0:00 named |
| 394 ? | S | 0:00 l1pd |
| 412 ? | S | 0:00 rpc.statd |
| 423 ? | SW | 0:00 [rpc.quotad] |
| 434 ? | SW | 0:00 [rpc.mount] |
| 449 ? | SW | 0:00 [nfsd] |
| 450 ? | SW | 0:00 [nfsd] |
| 451 ? | SW | 0:00 [nfsd] |
| 453 ? | SW | 0:00 [nfsd] |
| 454 ? | SW | 0:00 [nfsd] |
| 455 ? | SW | 0:00 [nfsd] |
| 456 ? | SW | 0:00 [nfsd] |
| 457 ? | SW | 0:00 [lockd] |
| 458 ? | SW | 0:00 [rpciod] |
| 493 ? | S | 0:00 sendmail: accepting on port 22 |
| 524 ? | S | 0:00 diald |
| 564 tty1 | SW | 0:00 [mingetty] |
| 565 tty2 | SW | 0:00 [mingetty] |
| 566 tty3 | SW | 0:00 [mingetty] |
| 567 tty4 | SW | 0:00 [mingetty] |
| 568 tty5 | SW | 0:00 [mingetty] |
| 569 tty6 | SW | 0:00 [mingetty] |
| 570 ? | S | 0:00 /etc/X11/config -daemon |
| 572 ? | S | 0:00 update (bflush) |
| 1197 ? | S | 0:00 smbd -D |
| 1208 ? | S | 0:01 smbd -D |
| 1216 ? | S | 0:00 in.telnet |
| 1710 ? | S | 0:00 |
| 1711 pts/3 | S | 0:00 login |
| 1725 pts/3 | S | 0:00 su - |
| 1729 pts/3 | S | 0:00 -bash |
| 1752 ? | S | 0:28 /usr/bin/X11/X -auth /var/gdm/:0.xauth |
| 1761 ? | S | 0:00 /etc/X11/config -daemon |
| 18466 ? | S | 0:00 bash -login /etc/X11/gdm/Sessions/Default |
| 18481 ? | S | 0:00 /usr/bin/gnome-session |
| 18503 ? | S | 0:00 gnome-proxy --client0 |
| 18509 ? | S | 0:01 enlightenment -client2 |
| 18522 ? | S | 0:00 panel --client8 |
| 18524 ? | S | 0:00 xscreensaver-no-splash -timeout 20 -nice |
| 18526 ? | S | 0:01 gmc-client10 |
| 18530 ? | S | 0:00 gnome-name-service |
| 18538 ? | S | 0:00 gnomepager-applet --activate-gserver |
| 18540 ? | S | 0:00 gen_util_applet --activate-gserver |
| 18547 ? | S | 0:00 gnome-terminal |
| 18548 ? | S | 0:00 gnome-pty-helper |
| 18549 pts/2 | S | 0:00 bash |
| 18577 pts/3 | R | 0:00 ps x |
| 18578 pts/3 | S | 0:00 more |

有多种方法可以消除运行中的各种守护进程。你可以删除守护进程本身、`/etc/rc.d`运行级别目录中的链接或启动脚本。我倾向于修改启动各种守护进程的脚本，因为这样可以通过脚本中添加注释来记录我做了什么以及为什么要这样做。这让计算机保持接近原始状态，对你或未来维护该系统的人很有帮助。（例如，如果简单地删除链接，记录你做了什么以及为什么将困难得多。）

以下步骤用于消除每个不必要的守护进程。请从上到下操作。第一批进程（列在方括号`[ ]`内）都是 Linux 内核的一部分（见第 4 章）。内核守护进程是下一节处理的第一个进程。`klogd`是 Linux 日志进程的一部分，我们想保留它。`crond`执行周期任务，我们也想保留它。在我看来，`inetd`、`named`（如果你安装了第1章中的可选 Red Hat 服务）、`lpd`、`sendmail`、`smbd`、`nmbd`守护进程对于防火墙服务器都是是不必要的。这些进程都与我的登录有关，更新进程外（它是内核的一部分）。来自控制台的`mingetty`进程不应引起任何安全问题。登录进程和`bash` shell（288 和 296）是从控制台以 root 登录并运行`bash` shell。你也可以忽略最后几个进程（308、323、324 和 336），因为它们是我以前通过 Telnet 远程登录（`in.telnet`）、然后切换到 root（`su`）、root 的 shell（`bash`）以及显示所有进程的命令（`ps x`）时使用的进程。不过，我将在稍后的“停止 inetd”部分中消除 Telnet 登录功能，但现在没关系，因为我仍在配置防火墙服务器。

以下章节描述了我如何配置我的防火墙服务器。

# 停止 inetd

其思想是尽可能消除安全漏洞。实现这一点的方法是运行尽可能少的守护进程。许多进程是由`inet`守护进程启动的。`inetd`被称为超级守护，因为它负责根据需要启动所有进程。让一个守护进程负责启动许多进程，意味着你只需要运行一个而不是多个。你要么完全不运行`inetd`，要么编辑它的配置文件。在我看来，运行`inetd`是最好的，因为这样对于什么存在、什么不存在将没有疑问。

- 1. 以 root 身份登录 atlas。有许多方法可以不运行`inetd`。首先，你可以通过登录 root 并输入以下命令移除执行权限：

- 2. 你也可以直接删除级别目录中的链接。例如，你可以删除`/etc/rc.d/S50inet`文件，它是`/etc/rc.d/init.d/inet`脚本的链接。如果没有该链接，启动计算机时将不会执行`inetd`脚本。

```
chmod -x /etc/rc.d/init.d/inet
```

- 3. 你也可以删除链接：

```
rm /etc/rc.d/rc3/S50inet

rm /etc/rc.d/rc4/S50inet

rm /etc/rc.d/rc5/S50inet
```

你也可以简单地重命名链接，这样它们就不会被执行，但如果你决定重启它们，你会知道它们应该是什么名字。

```
mv /etc/rc.d/rc3/S50inet /etc/rc.d/rc3_/S50inet

mv /etc/rc.d/rc5/S50inet /etc/rc.d/rc5_/S50inet
```
