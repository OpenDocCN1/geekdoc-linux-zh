
## HP-UX 示例（部分列表）

```
# ps -ef

UID PID PPID C STIME TTY TIME COMMAND
root 0 0 0 Mar 9 ? 107:28 swapper
root 1 0 0 Mar 9 ? 2:27 init
root 2 0 0 Mar 9 ? 14:13 vhand
root 3 0 0 Mar 9 ? 114:55 statdaemon
root 4 0 0 Mar 9 ? 5:57 unhashdaemon
root 7 0 0 Mar 9 ? 154:33 ttiser
root 70 0 0 Mar 9 ? 0:01 lvmkd
root 71 0 0 Mar 9 ? 0:01 lvmkd
root 72 0 0 Mar 9 ? 0:01 lvmkd
root 13 0 0 Mar 9 ? 9:54 vx_sched_thread
root 14 0 0 Mar 9 ? 1:54 vx_iflush_thread
root 15 0 0 Mar 9 ? 2:06 vx_irise_thread
root 16 0 0 Mar 9 ? 2:27 vx_inactive_cache_thread
root 17 0 0 Mar 9 ? 0:40 vx_delxlwri_thread
root 18 0 0 Mar 9 ? 0:33 vx_logflush_thread
root 19 0 0 Mar 9 ? 0:07 vx_attrsync_thread
.
.
root 69 0 0 Mar 9 ? 0:09 vx_inactive_thread
root 73 0 0 Mar 9 ? 0:01 lvmkd
root 74 0 0.19 Mar 9 ? 3605:29 netsr
root 75 0 0 Mar 9 ? 0:18 netsr
root 76 0 0 Mar 9 ? 0:17 netsr
root 77 0 0 Mar 9 ? 0:14 netsr
root 78 0 0 Mar 9 ? 0:48 nvisr
root 79 0 0 Mar 9 ? 0:00 susp sched
root 80 0 0 Mar 9 ? 0:00 smsch ed
root 81 0 0 Mar 9 ? 0:00 smsch ed
root 82 0 0 Mar 9 ? 0:00 blksch ed
root 83 0 0 Mar 9 ? 0:00 blksch ed
root 84 0 0 Mar 9 ? 0:00 strm ed
root 85 0 0 Mar 9 ? 0:00 stre wd
root 3730 1 0 16:39:22 console 0:00 /usr/sbin/getty console console
root 404 1 0 Mar 9 ? 3:57 /usr/sbin/swagentd
oracle 919 1 0 15:23:23 ? 0:00 oracleprcd (LOCAL=NO)
root 289 1 2 Mar 9 ? 78:34 /usr/sbin/sync er
root 426 1 0 Mar 9 ? 0:10 /usr/sbin/syslogd -D
root 576 1 0 Mar 9 ? 0:00 /usr/sbin/portmap
root 429 1 0 Mar 9 ? 0:00 /usr/sbin/pythdaemon
root 590 1 0 Mar 9 ? 0:00 /usr/sbin/biod 4
root 442 1 0 Mar 9 ? 0:00 /usr/lib/nkml/daemon 0 0 0 0 0 1 -2
oracle 8145 1 0 12:02:48 ? 0:00 oracleprgd (LOCAL=NO)
root 591 1 0 Mar 9 ? 0:00 /usr/sbin/biod 4
root        589    1  0 Mar  9 ?  0:00 /usr/sbin/biod 4
root        592    1  0 Mar  9 ?  0:00 /usr/sbin/biod 4
root        604    1  0 Mar  9 ?  0:00 /usr/sbin/rpc.lockd
root        598    1  0 Mar  9 ?  0:00 /usr/sbin/rpc.statd
root        610    1  0 Mar  9 ?  0:16 /usr/sbin/autumount -f /etc/auto_master
root        638    1  0 Mar  9 ?  0:06 sendmail: accepting connections
root        618    1  0 Mar  9 ?  0:02 /usr/sbin/inetd
root        645    1  0 Mar  9 ?  5:01 /usr/sbin/snmpd
root        661    1  0 Mar  9 ? 11:28 /usr/sbin/fddisubagtd
root        711    1  0 Mar  9 ? 30:59 /opt/dce/sbin/rpcd
root        720    1  0 Mar  9 ?  0:00 /usr/sbin/vtadaemon
root        867   777  1  0 Mar  9 ?  0:00 <defunct>
lp          733    1  0 Mar  9 ?  0:00 /usr/sbin/lpsched
root        777    1  0 Mar  9 ?  8:55 DIAGON
root        742    1  0 Mar  9 ?  0:15 /usr/sbin/cron
oracle      7880    1  0 11:43:47 ?  0:00 oracle@grpd (LOCAL=NO)
root        842    1  0 Mar  9 ?  0:00 /usr/vue/bin/vue login
oracle      5625    1  0 07:00:14 ?  0:01 ora_smon_@prd
root        781    1  0 Mar  9 ?  0:00 /usr/sbin/envd
root        833   777  0 Mar  9 ?  0:00 DEMLOG  DEMLOG;0;0;
root        813    1  0 Mar  9 ?  0:00 /usr/sbin/nfsd 4
root        807    1  0 Mar  9 ?  0:00 /usr/sbin/rpc.mountd
root        815   813  0 Mar  9 ?  0:00 /usr/sbin/nfsd 4
root        817   813  0 Mar  9 ?  0:00 /usr/sbin/nfsd 4
root        835   777  0 Mar  9 ?  0:13 PSMON  PSMON;PSMON;0;0;
```

### 标题说明

- `UID`：进程所有者的用户 ID。
- `PID`：进程 ID（你可以使用此编号来终止进程）。
- `PPID`：父进程的进程 ID。
- `C`：用于调度的进程利用率。
- `STIME`：进程的启动时间。
- `TTY`：进程的 controlling terminal（控制终端），如果有的话。
- `TIME`：进程的累计执行时间。
- `COMMAND`：命令名称和参数。

`ps` 可以快速概况你系统上正在运行的进程。若要获取更详细的信息，你可以包含 `l` 选项，该选项包含许多有用的额外信息，如下例所示：

在此示例中，第一列是用于标志的 `F`。`F` 提供了关于进程是否已交换、是否位于核心内存、是否为系统进程等信息的八进制值。八进制值在不同系统间有时会有所不同，因此请查阅你所在系统的手册页以查看标志的八进制值。
