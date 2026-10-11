

![](img/8ad518fddafc7f5e73715a2604b61d50_61_0.png)

> 欲了解关于网络的更多信息，请参阅第11章。

## 保持记录

保持准确、定期记录能使网络管理变得更加容易。记录包括日志文件、每日日志和事故报告。通常，问题或故障发生在无人值守的时候，而那时被假设什么都没发生。实际上，许多任务被安排在凌晨执行，而灾难发生的高峰期恰恰是无人掌舵、无法将系统引向安全区域的时候。确保所有进程和系统变更都被人工和机器记录在案，可以在灾后调查中节省数小时。查阅日志文件以查看发生了什么，可以迅速确定单点故障，并使你在几分钟内恢复系统。这比进行“软件巫术”或采取诸如重新安装操作系统等极端措施要愉快得多。

### 日志文件

保留日志文件的硬拷贝和软拷贝有助于你排查任何问题，并稳定地记录系统发生了什么。在 Linux 中，存在几个重要的日志文件。这些包括 /var/adm/syslog、/var/adm/messages、/var/adm/kernel 和 /var/log。偶尔，你需要从日志文件中回收一些磁盘空间。为了截断文件，你首先需要查明记录守护进程 klogd 的进程号，然后将其终止（kill）。否则，如果你在尝试删除或编辑该文件时进程仍在向其 inode 写入数据，文件空间就不会被释放。终止 klogd 后，你可以编辑日志，但请务必在之后重启 klogd。清单 2-1 展示了 /var/adm/syslog 的一个示例。

**清单 2–1：** 查看 /var/adm/syslog

```text
Jul  7 15:38:44 tigerden ps[13781]: warning: can't get client address:
    Connection reset by peer
Jul  7 15:39:05 tigerden inetd[58]: ftp/tcp server failing (looping), service
    terminated
Jul  7 15:39:13 tigerden inetd[13900]: time/tcp: bind: Address already in use
Jul  7 15:39:13 tigerden inetd[13900]: telnet/tcp: bind: Address already in use
Jul  7 15:39:13 tigerden inetd[13900]: pop3/tcp: bind: Address already in use
Jul  7 15:39:13 tigerden inetd[13900]: imap2/tcp: bind: Address already in use
Jul  7 15:39:13 tigerden inetd[13900]: auth/tcp: bind: Address already in use
Jul  7 15:39:43 tigerden inetd[13905]: time/tcp: bind: Address already in use
Jul  7 15:39:43 tigerden inetd[13905]: ftp/tcp: bind: Address already in use
Jul  7 15:39:43 tigerden inetd[13905]: telnet/tcp: bind: Address already in use
Jul  7 15:39:43 tigerden inetd[13905]: pop3/tcp: bind: Address already in use
Jul  7 15:39:43 tigerden inetd[13905]:  imap2/tcp: bind: Address already in use
Jul  7 15:39:43 tigerden inetd[13905]:  auth/tcp: bind: Address already in use
Jul  7 15:40:29 tigerden syslog: error: cannot execute /usr/sbin/imapd: No such file or directory
Jul  7 15:40:50 tigerden syslog: error: cannot execute /usr/sbin/imapd: No such file or directory
Jul  7 15:40:57 tigerden sendmail[13959]: NOQUEUE: "wiz" command from root@localhost [127.0.0.1] (127.0.0.1)
Jul  7 15:40:57 tigerden sendmail[13959]: NOQUEUE: "debug" command from root@localhost [127.0.0.1] (127.0.0.1)
Jul  7 15:41:42 tigerden ps[13995]: warning: can't get client address: Connection reset by peer
Jul  7 15:41:42 tigerden ps[13996]: warning: can't get client address: Connection reset by peer
Jul  7 15:41:42 tigerden ps[13999]: warning: can't get client address: Connection reset by peer
Jul  7 15:43:10 tigerden login[14213]: REPEATED login failures on `ttyd' from `localhost'
Jul  7 15:43:10 tigerden login[14214]: REPEATED login failures on `ttyp1' from `localhost'
Jul  7 15:43:10 tigerden login[14220]: REPEATED login failures on `ttyy4' from `localhost'
Jul  7 15:43:10 tigerden login[14222]: REPEATED login failures on `ttyp5' from `localhost'
Jul  7 15:43:10 tigerden login[14223]: REPEATED login failures on `ttyp6' from `localhost'
Jul  7 15:43:25 tigerden login[14228]: REPEATED login failures on `ttyp0' from `localhost'
Jul  7 15:43:25 tigerden login[14229]: REPEATED login failures on `ttyp1' from `localhost'
Jul  7 15:43:25 tigerden login[14236]: REPEATED login failures on `ttyp4' from `localhost'
Jul  7 15:43:25 tigerden login[14237]: REPEATED login failures on `ttyp5' from `localhost'
```

清单 2-2 展示了 /var/adm/messages 的一个示例。

**清单 2-2：** 查看 /var/adm/messages

```text
Aug  6 11:01:42 tigerden syslogd 1.3-3: restart.
Aug  6 11:01:43 tigerden kernel: klogd 1.3-3, log source = /proc/kmsg started.
Aug  6 11:01:44 tigerden kernel: Loaded 5892 symbols from /boot/System.map.
Aug  6 11:01:44 tigerden kernel: Symbols match kernel version 2.0.34.
Aug  6 11:01:44 tigerden kernel: Loaded 25 symbols from 10 modules.
Aug  6 11:01:44 tigerden kernel: Swansea University Computer Society NET3.035 for Linux 2.0
Aug  6 11:01:44 tigerden kernel: NET3: Unix domain sockets 0.13 for Linux NET3.035.
Aug  6 11:01:44 tigerden kernel: VFS: Diskquotas version dquot_5.6.0 initialized
Aug  6 11:01:44 tigerden kernel: Intel Pentium with F0 OF bug - workaround enabled.
Aug  6 11:01:44 tigerden kernel: Serial driver version 4.13 with no serial options enabled
Aug  6 11:01:44 tigerden kernel: tty00 at 0x03f8 (irq = 4) is a 16550A
Aug  6 11:01:44 tigerden kernel: tty02 at 0x03e8 (irq = 4) is a 16550A
Aug  6 11:01:44 tigerden kernel: Floppy drive(s): fd0 is 1.44M
Aug  6 11:01:44 tigerden kernel: FDC 0 is a post-1991 82077
Aug  6 11:01:44 tigerden kernel: Ipl at 0x0378. (polling)
Aug  6 11:01:44 tigerden kernel: CSLIP: code copyright 1989 Regents of the University of California
Aug  6 11:01:44 tigerden kernel: SLIP: version 0.8.4-NET3.019-NETWTY-MODULAR (dynamic channels, max=256).
Aug  6 11:01:44 tigerden kernel: PPP: version 2.2.0 (dynamic channel allocation)
Aug  6 11:01:44 tigerden kernel: PPP Dynamic channel allocation code copyright 1995 Caldera, Inc.
Aug  6 11:01:44 tigerden kernel: PPP line discipline registered.
Aug  6 11:01:44 tigerden kernel: PS/2 auxiliary pointing device detected - driver installed.
Aug  6 11:01:44 tigerden kernel: Linux PCMCIA Card Services 3.0.0
Aug  6 11:01:44 tigerden kernel: kernel build: 2.0.34 #2 Thu Jun 4 22:27:11 PDT 1998
Aug  6 11:01:44 tigerden kernel: options: [cardbus]
Aug  6 11:01:44 tigerden kernel: Intel PCIC probe:
Aug  6 11:01:44 tigerden kernel: TI 1131 Cardbus at 0x3e0 of 0x00, mem 0x68000000, 2 sockets
Aug  6 11:01:44 tigerden kernel: host opts [0]: [ring] [serial irq] [pci irq] [lat 32/176] [bus 32/34]
Aug  6 11:01:44 tigerden kernel: host opts [1]: [ring] [serial irq] [pci irq] [lat 32/176] [bus 35/37]
Aug  6 11:01:44 tigerden kernel: ISA irqs (scanned) = 3.4.10 polled status, interval = 1000 ms
Aug  6 11:01:44 tigerden kernel: cs: I/O port probe 0x0100-0x03ff: excluding 0x210-0x217 0x220-0x22f 0x290-0x297 0x380-0x38f
Aug  6 11:01:44 tigerden kernel: cs: I/O port probe 0x0a00-0x0aff: clean.
Aug  6 11:01:44 tigerden kernel: cs: memory probe 0x0d0000-0x0dffff: clean.
Aug  6 11:01:44 tigerden kernel: eth0: 3Com 5c89, port 0x300, irq 3, Auto port, hw_addr 00:60:08:82:E9:0E
Aug  6 11:01:44 tigerden kernel: tty01 at 0x02f8 (irq = 10) is a 16550A
Aug  6 11:01:49 tigerden kernel: 1BC5: socksys registered on character major 30
Aug  6 11:01:55 tigerden login[115]: ROOT LOGIN on 'tty1'
Aug  6 11:02:03 tigerden passwd[127]: password for 'root' changed by 'root'
Aug  6 11:21:42 tigerden -- MARK --
Aug  6 11:38:04 tigerden init: Switching to runlevel: 6
Aug  6 11:39:02 tigerden syslogd 1.3-3: restart.
Aug  6 11:39:03 tigerden kernel: klogd 1.3-3. log source = /proc/kmsg started.
Aug  6 11:39:04 tigerden kernel: Loaded 5892 symbols from /boot/System.map.
Aug  6 11:39:04 tigerden kernel: Symbols match kernel version 2.0.34.
Aug  6 11:39:04 tigerden kernel: Loaded 25 symbols from 10 modules.
Aug  6 11:39:04 tigerden kernel: Swansea University Computer Society NET3.035 for Linux 2.0
Aug  6 11:39:04 tigerden kernel: NET3: Unix domain sockets 0.13 for Linux NET3.035.
Aug  6 11:39:04 tigerden kernel: VFS: Diskquotas version dquot_5.6.0 initialized
Aug  6 11:39:04 tigerden kernel: Intel Pentium with F0 OF bug - workaround enabled.
Aug  6 11:39:04 tigerden kernel: Serial driver version 4.13 with no serial options enabled
Aug  6 11:39:04 tigerden kernel: tty00 at 0x03f8 (irq = 4) is a 16550A
Aug  6 11:39:04 tigerden kernel: tty02 at 0x03e8 (irq = 4) is a 16550A
Aug  6 11:39:04 tigerden kernel: Floppy drive(s): fd0 is 1.44M
Aug  6 11:39:04 tigerden kernel: FDC 0 is a post-1991 82077
Aug  6 11:39:04 tigerden kernel: lpc at 0x0378, (polling)
Aug  6 11:39:04 tigerden kernel: CSLIP: code copyright 1989 Regents of the University of California
Aug  6 11:39:04 tigerden kernel: SLIP: version 0.8.4-NET3.019-NEWTTY-MODULAR (dynamic channels, max=256).
Aug  6 11:39:04 tigerden kernel: PPP: version 2.2.0 (dynamic channel allocation)
Aug  6 11:39:04 tigerden kernel: PPP Dynamic channel allocation code copyright 1995 Caldera, Inc.
```

### 每日日志

写下当天与系统相关的事件（请只记录系统相关事项——把你那位可爱同事的个人感想留给自己）。系统日志使你可以追踪系统故障、可疑活动和性能的趋势。如果你定期提交状态报告，它也是一个很有用的资源。当系统在故障后管理层逼你给出答案时，你的记录可以反映出那些可能被你遗忘的细微细节！

### 记录事故

每当出现问题（如电源故障、文件损坏、入侵者扫描你的网络等）时，都要做一个记录。这个记录至关重要，尤其是如果

