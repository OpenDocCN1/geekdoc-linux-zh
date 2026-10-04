# Playing with the Shell 97

In this case, the system is running Linux kernel version 2.6.5.

To read a file, use the more command. Here's an example:

```
more /etc/passwd
root:x:0:0:root:/bin/bash
bin:x:1:1:bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
... deleted ...
```

To see a list of all the programs running on the system, use the ps
command, like this:

| PID TTY STAT TIME COMMAND |
| 1 ? S 0:05 init [5] |
| 2 ? SWN 0:00 [ksoftirqd/0] |
| 3 ? SW 0:00 [events/0] |
| 4 ? SW 0:00 [blockd/0] |
| 5 ? SW 0:00 [pdfflush] |
| 6 ? SW 0:00 [pdfflush] |
| 8 ? SW 0:00 [aio/0] |
| 7 ? SW 0:00 [kswapod] |
| 9 ? SW 0:00 [kseriod] |
| 13 ? SW 0:00 [kjjournal] |
| 98 ? SW 0:00 [thudbd] |
| 222 ? SW 0:00 [usb-storage] |
| 223 ? SW 0:00 [scsi_eh_0] |
| 759 ? SW 0:00 [journal] |
| 2177 ? S 0:00 [/sbin/dhclient -1 -q -lf] |

```
/var/lib/dhcp/dhclient-eth0.pid -cp /var/run/dhclient-eth0 -cf /etc/dhclient.conf eth0
2226 ? S 0:00 syslog -m 0
2230 ? S 0:00 klod -x
2258 ? S 0:00 portmap
2278 ? S 0:00 rpc.statd
... lines deleted ...
```

Amazing how many programs that can run on a system even when only
are logged in as a user, isn't it?

As you can guess, you can do everything from a shell prompt, but it does
take some getting used.