
# 第11 章 UNIX 性能工具 man page

![](img/6969df54e516231f8e64fd1177ac1127_752_0.png)

![](img/6969df54e516231f8e64fd1177ac1127_753_0.png)

`root $ ps -ef`

| UID | PID | PPID | C | STIME | TIME | CMD |
|---|---|---|---|---|---|---|
| root | 1479 | 0 | C | Feb 18 | 00:17 | `/usr/sbin/asytmon` |
| root | 10995 | 0 | C | Jun 01 | 00:00 | `/bin/btfd` |
| root | 7468 | 0 | C | Feb 24 | 00:13 | `/opt/perf/pivald` |
| root | 16763 | 16731 | 0 | 07:46 pts/4 | 0:00 | `/usr/dt/bin/dtlogin` |
| root | 484 | 478 | 0 | Feb 18 | 00:00 | `/opt/perf/bibild` |
| root | 16792 | 3059 | 0 | 07:50 | 20:06 | `/usr/dt/bin/snmp` |
| root | 473 | 0 | C | Feb 18 | 00:07 | `/usr/lib/bin/smis` |
| root | 474 | 0 | C | Feb 18 | 00:00 | `/usr/lib/bin/dpmid` |
| root | 485 | 458 | 0 | Feb 18 | 73:49 | `mial -r -p 32874` |

| UID | PID | PPID | C | STIME | TIME | CMD |
|---|---|---|---|---|---|---|
| root | 2954 | 2936 | 0 | Feb 22 | 00:01 | `/bin/usr/bin/Xsession` |
| root | 2936 | 2266 | 0 | Feb 22 | 00:00 | `/usr/dt/bin/dtlog -daemon` |
| root | 3061 | 2035 | 0 | Feb 22 | 01:32 | `dcstart` |
| root | 3058 | 1035 | 0 | Feb 22 | 00:01 | `/usr/dt/bin/dttss` |
| root | 2712 | 133 | 0 | Feb 22 | 00:01 | `/usr/sbin/cron` |
| root | 11001 | 11000 | 0 | Feb 22 | 00:00 | `<defunct>` |
| root | 2938 | 2954 | 0 | Feb 22 | 00:01 | `/usr/open/bin/fbconsole -d :0` |
| root | 3059 | 3002 | 0 | Feb 22 | 00:00 | `/usr/sbin/shell -c unit` |
| root | 3063 | 3059 | 0 | Feb 22 | 28:35 | `/usr/dt/bin/dthelview -helpvol` |
| root | 110095 | 10995 | 0 | Feb 22 | 00:00 | `/usr/lib/dt/dtgeometry` |
| root | 3002 | 2999 | 0 | Jun 01 | 00:02 | `/opt/perb/bin/agdbster -t al-` |
| root | 3072 | 133 | 0 | Feb 22 | 00:01 | `DISPLIG` |
| root | 3062 | 3059 | 0 | Feb 22 | 01:37 | `rsatad` |
| root | 3967 | 1000 | 0 | Feb 22 | 00:00 | `/usr/dt/bin/filegeometry -700` |
| root | 3008 | 3000 | 0 | Feb 22 | 00:00 | `/usr/dt/bin/dtvolcdckm` |
| root | 3078 | 3067 | 0 | Feb 22 | 00:00 | `/usr/dt/bin/dsdm` |
| root | 10488 | 1111 | 0 | Feb 22 | 12:00 | `/bin/cat/tmp/removable/notify0` |
| root | 16761 | 133 | 0 | 07:46:45 | 12:00 | `/usr/perf/bin/dcd -b` |
| root | 2208 | 1522 | 0 | Feb 24 | 05:07 | `/etc` |
| root | 2664 | 0 | Feb 24 | 00:00 | `/usr/dt/bin/dtlog -daemon` |
| root | 2882 | 0 | Feb 24 | 15:41 | `/usr/sbin/syncd` |
| root | 3624 | 2664 | 0 | Feb 24 | 00:00 | `/usr/lib/bin/ -D` |
| root | 3624 | 2664 | 0 | Feb 24 | 00:00 | `dtlogin <0>` |
| root | 3950 | 1 | 0 | Feb 24 | 55:50 | `/usr/perf/bin/libid` |
| root | 4154 | 1 | 0 | Feb 24 | 00:00 | `/usr/perf/bin/libid` |
| root | 4490 | 1 | 0 | Feb 24 | 00:48 | `/usr/lib/bin/perfib` |
| root | 5172 | 1 | 0 | Feb 24 | 00:00 | `/usr/dt/bin/dtdaemon` |
| root | 5724 | 5172 | 0 | Feb 24 | 09:54 | `/usr/sbin/sylsd` |
| root | 6242 | 5172 | 0 | Feb 24 | 01:04 | `/usr/dt/bin/dtquery` |
| root | 6450 | 5172 | 0 | Feb 24 | 00:02 | `connections` |
| root | 6710 | 5172 | 0 | Feb 24 | 07:36 | `/usr/sbin/portmap` |
| root | 7224 | 5172 | 0 | Feb 24 | 01:09 | `/usr/sbin/timed -S` |
| root | 8000 | 5172 | 0 | Feb 24 | 11:55 | `msysd/msysmd` |
| root | 8516 | 8782 | 0 | Feb 24 | 00:00 | `fmt -c` |
| root | 8854 | 8000 | 0 | Feb 24 | 00:00 | `/usr/dt/bin/ntl_reader 1` |
| root | 9036 | 8000 | 0 | Feb 24 | 10:09 | `ovydwd -0 -n5000` |
| root | 9228 | 8000 | 0 | Feb 24 | 04:44 | `pm -Au -Mt -mt` |
| root | 9804 | 8000 | 0 | Feb 24 | 02:28 | `traf` |
| root | 10320 | 8000 | 0 | Feb 24 | 00:33 | `overmsd` |
| root | 10578 | 8000 | 0 | Feb 24 | 00:13 | `zertprod -O` |
| root | 11094 | 8000 | 0 | Feb 24 | 17:50 | `netroman -P` |
| root | 11352 | 8000 | 0 | Feb 24 | 00:02 | `smnpcollect` |
| root | 11598 | 8000 | 0 | Feb 24 | 00:25 | `/usr/sbin/bin/cron` |
| root | 12140 | 5172 | 0 | Feb 24 | 00:01 | `/usr/lib/netvsc/yp/bind` |
| root | 12652 | 5172 | 0 | Feb 24 | 01:39 | `/usr/sbin/rcmp.mount` |
| root | 12908 | 5172 | 0 | Feb 24 | 00:00 | `/usr/sbin/rcmp.stat` |
| root | 13428 | 5172 | 0 | Feb 24 | 00:00 | `/usr/sbin/bin/unfrintd` |
| root | 14190 | 5172 | 0 | Feb 24 | 72:59 | `/usr/sbin/automountd` |
| root | 14552 | 5172 | 0 | Feb 24 | 00:00 | `/usr/dt/bin/dtdaemon` |
