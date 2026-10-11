
```text
root 70 Mar 5 0:04 lvmdk
root 71 Mar 9 0:01 lvmdk
root 72 Mar 9 0:01 lvmdk
root 73 Mar 9 5:54 vx_sch_ed thread
root 74 Mar 9 1:54 vx_iflush_thread
root 75 Mar 9 2:06 vx_free_thread
root 76 Mar 9 2:12 vx_inactive_cache_thread
root 77 Mar 9 0:40 vx_bowril_thread
root 78 Mar 9 ? 0:33 vx_iflush_thread
root 79 Mar 9 ? 0:07 vx_logfsync_thread
root 80 0 0 Mar 9 ? 0:09 vx_inactive_thread
root 81 0 0 Mar 9 ? 0:01 lvmdk
root 82 0 0 Mar 9 ? 0:57 netiser
root 83 0 0 Mar 9 ? 0:18 netiser
root 84 0 0 Mar 9 ? 0:49 netiser
root 85 0 0 Mar 9 ? 0:14 netiser
root 86 0 0 Mar 9 ? 0:48 nvsrler
root 87 0 0 Mar 9 ? 0:00 smpsched
root 88 0 0 Mar 9 ? 0:00 smpsched
root 89 0 0 Mar 9 ? 0:00 smpsched
root 90 0 0 Mar 9 ? 0:00 skbksched
root 91 0 0 Mar 9 ? 0:00 stmmem
root 92 0 0 Mar 9 ? 0:00 strmled
root 100 1 0 1:15:22 console 0:00 /usr/sbin/getty getty console
root 101 1 0 Mar 9 ? 1:57 /usr/sbin/xawgettyd
oracle 102 1 0 5:14:23 ? 0:00 oracle_sprd (LOCAL-NO)
root 103 1 0 Mar 9 ? 78:34 /usr/sbin/rpcd rayer
root 104 1 0 Mar 9 ? 0:10 /usr/sbin/spind -D
root 105 1 0 Mar 9 ? 0:00 /usr/sbin/portmap
root 106 1 0 Mar 9 ? 0:00 /usr/sbin/gsfsdemon
root 107 1 0 Mar 9 ? 0:00 /usr/sbin/blogd 4
root 108 1 0 Mar 9 ? 0:00 /usr/sbin/nkl_daemond 0 0 0 0 0 1 2
oracle 109 1 0 1:13:43 ? 0:00 oracle_sprd (LOCAL-NO)
root 110 1 0 Mar 9 ? 0:00 /usr/sbin/tnsd
root 111 1 0 Mar 9 ? 0:00 /usr/sbin/bload 4
root 112 1 0 Mar 9 ? 0:00 /usr/sbin/bload 4
root 113 1 0 Mar 9 ? 0:00 /usr/sbin/rpc_lockd
root 114 1 0 Mar 9 ? 0:00 /usr/sbin/rpc_atstat
root 115 1 0 Mar 9 ? 0:16 /usr/sbin/automount -f /etc/auto_master
root 116 1 0 Mar 9 ? 0:06 aendmail: accepting connections
root 117 1 0 Mar 9 ? 0:02 /usr/sbin/inetd
root 118 1 0 Mar 9 ? 5:01 /usr/sbin/snmpd
root 119 1 0 Mar 9 ? 11:28 /usr/sbin/ttdbgdapt
root 120 1 0 Mar 9 ? 30:55 lpcp/deco/tpc/rpcd
root 121 1 0 Mar 9 ? 0:00 /usr/sbin/vtfsdemon
root 122 1 0 Mar 9 ? 0:00 <default>
root 123 1 0 Mar 9 ? 0:00 <default>
root 124 1 0 Mar 9 ? 8:55 DIAGMON
root 125 1 0 Mar 9 ? 0:15 /usr/sbin/cron
oracle 126 1 0 1:14:37 ? 0:00 oracle_sprd (LOCAL-NO)
root 127 1 0 Mar 9 ? 0:00 /usr/sbin/dnsmgrd
oracle 128 1 0 07:00:14 ? 0:01 ora_smons_prd
root 129 1 0 Mar 9 ? 0:00 /usr/sbin/envd
root 130 1 0 Mar 9 ? 0:00 DSBLOG; DSBLOG;DNSLOG;0;0
root 131 1 0 Mar 9 ? 0:00 /usr/sbin/nsfd 4
root 132 1 0 Mar 9 ? 0:00 /usr/sbin/nsfs_mount
root 133 1 0 Mar 9 ? 0:00 /usr/sbin/nsfd 4
root 134 1 0 Mar 9 ? 0:00 /usr/sbin/nsfd 4
root 135 1 0 Mar 9 ? 0:13 PSMS;PSM;0;0;1
```

以下是对各表头的简要说明：

- `UID`：进程所有者的用户 ID。
- `PID`：进程 ID（你可以使用此数字来终止进程）。
- `PPID`：父进程的进程 ID。
- `C`：处理器利用率。在多处理器系统上，你可能会看到这个数字超过 100%。它可能会达到每个处理器 100%，因此双处理器系统可能显示 200% 的利用率。这取决于不同的 UNIX 变体。
- `STIME`：进程启动时间。
- `TTY`：进程的控制终端。
- `TIME`：进程的累计执行时间。
- `COMMAND`：命令名称及参数。

`ps` 提供了系统中正在运行的进程的简要概况。要获取更详细的信息，你可以包含 `-f` 选项，其中包含许多有用的额外信息，如下例所示：
