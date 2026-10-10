
## HP-UX 示例（部分列表）

```text
marty% $ ps -ef

    PID    PPID STIME TTY TIME COMMAND
    0      0    Mar 7  ?  107:28 swapper
    1      0    Mar 9  ?  2:27 init
    2      0    Mar 9  ?  14:13 vanda
    3      0    Mar 9  ?  11:43:58 ata/daemon
    4      0    Mar 9  ?  5:57 unhashed
    7      0    Mar 9  ?  154:33 ttsh
```

```text
root 6710 5172 0 Feb 24 - 7.34 /usr/sbin/portmap
root 6956 5172 0 Feb 24 - 0.02 /usr/sbin/initnd
root 7224 5172 0 Feb 24 - 1.08 /usr/sbin/timed -G
root 7842 5172 0 Feb 24 - 11.55 /usr/sbin/smpd
root 8000 1 0 Feb 24 - 0.00 netif
root 8512 8782 1 0 Feb 24 - 9.00 telnet -Cf
root 8782 1 0 Feb 24 - 0.00 /usr/OB/NTU-nti_reader o 1 1 1
root 9036 8000 0 Feb 24 - 10.09 otwdab o -8000
root 9288 8000 0 Feb 24 - 0.44 pcd -A -G -M -Mc -M -M
root 9848 8000 0 Feb 24 - 0.00 trapped -f
root 9804 8000 0 Feb 24 - 0.28 trapd
root 10062 8000 0 Feb 24 - 0.47 orstd
root 10232 8000 0 Feb 24 - 0.31 otwsmd
root 10578 8000 0 Feb 24 - 0.30 otelnd
root 10936 8000 0 Feb 24 - 0.18 otwsmd -O
root 11094 8000 0 Feb 24 - 17.50 netmon -P
root 11852 8000 0 Feb 24 - 0.02 smmpCollect
root 13954 1 0 Feb 24 - 1.22 /usr/sbin/cron
root 12140 5172 0 Feb 24 - 0.01 /usr/lib/tcp/netvcg/ypp/piped
root 12394 5172 0 Feb 24 - 1.28 /usr/sbin/tcp mountd
root 12652 5172 0 Feb 24 - 0.29 /usr/sbin/nfsd 8
root 12908 5172 0 Feb 24 - 0.00 /usr/sbin/rpc.statd
root 13166 5172 0 Feb 24 - 0.53 /usr/sbin/rpc.lockd
root 13428 1 0 Feb 24 - 0.00 /usr/sbin/printfixd
root 14190 5172 0 Feb 24 - 72.59 /usr/sbin/autoconfd
root 14452 5172 0 Feb 24 - 0.17 /usr/sbin/glqademon
root 14714 5172 0 Feb 24 - 0.00 /usr/sbin/rttstatd
root 14992 1 0 Feb 24 - 255.26 /usr/ipp/part/bin/scopeuse
root 15520 3624 1 Feb 24 - 15.29 /usr/df/bin/dtasensorn
root 15998 1 0 Feb 24 1f/0 - 0.00 /usr/bin/diagnostics/bin/diagd
root 16304 18682 0 Feb 24 pte/0 - 0.00 /usr/sbin/getty /dev/console
root 16774 1 Feb 24 pte/0 - 0.00 /bin/ksh
root 17092 4490 0 Feb 24 - 0.00 /usr/ipp/perl/bin/idd
root 27870 18186 1 Mar 25 - 68.54 /usr/ipp/perl/bin/rep_server -t
root 17630 15520 0 Mar 25 - 0.00 <defunct>
root 17898 15520 0 Mar 25 - 0.00 /usr/dt/bin/dtexec -open 0 -ttlp
root 18138 19888 0 Mar 24 pta/1 - 0.00 /usr/dt/bin/dtexec -open 0 -ttlp
root 18166 696 0 Mar 24 - 0.00 /usr/kall
root 18446 15520 0 Mar 15 - 0.00 rpc:ttdserver 100083 1
root 18892 15520 0 Mar 24 - 0.01 /usr/dt/bin/dtexec -open 0 -ttlp
root 19186 16304 0 Feb 24 pts/0 - 3.46 /usr/dt/bin/dtxterm
root 19450 1 0 Feb 24 - 0.01 /usr/XP/11/bin/namixt
root 19864 2208 0 Feb 24 - 0.00 /usr/dt/bin/dtexec -open 0 -ttlp
root 19888 19684 0 Feb 24 - 0.00 /usr/dt/bin/dxserver
root 20104 15520 0 Feb 27 - 0.00 /usr/dt/bin/dtexec -open 0 -ttlp
root 20248 20104 0 Feb 27 - 0.03 /usr/dt/bin/dtexec -open 0 -ttlp
root 20942 29708 0 Mar 14 - 0.03 /usr/dt/bin/dxscreen
root 20912 26306 0 Apr 05 - 0.03 /usr/dt/bin/dxscreen
root 33528 0 May 18 - 3.28 /usr/atria/etc/lockmgr a /var/
root 33834 3666 0 Mar 24 - 0.00 telnetd
root 34072 0 May 18 - 0.00 /usr/atria/etc/sdd_server
marrip 56296 36603 13:07:35.07 pts/2 - 0.00 pss -ef
marrip 36608 33834 1:07:55:50 pts/2 - 0.00 /bin/ksh
root 37220 15520 0 May 28 - 0.00 /usr/dt/bin/dtexec -open 0 -ttlp
INITPID: 1
```

### 使用 ps 检查进程

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

- **UID**：进程所有者的用户 ID。
- **PID**：进程 ID（你可以使用此数字来终止进程）。
- **PPID**：父进程的进程 ID。
- **C**：处理器利用率。在多处理器系统上，你可能会看到这个数字超过 100%。它可能会达到每个处理器 100%，因此双处理器系统可能显示 200% 的利用率。这取决于不同的 UNIX 变体。
- **STIME**：进程启动时间。
- **TTY**：进程的控制终端。
- **TIME**：进程的累计执行时间。
- **COMMAND**：命令名称及参数。

`ps` 提供了系统中正在运行的进程的简要概况。要获取更详细的信息，你可以包含 `-f` 选项，其中包含许多有用的额外信息，如下例所示：

```text
martyp $ ps -efl
F S UID PID PPID C PRI NI ADDR SZ WCHAN STIME TTY D
19 S 0 root 0 0 0 0 FY f5e6277f3 0 Feb 18 ? D
6 S 0 root 1 0 0 41 20 f5b96888 175 Feb 18 7 ? D
19 S 0 root 2 0 0 0 SY f5b96008 0 f02f8f3d Feb 18 ? ?
19 S 0 root 3 0 0 0 SY f5b960a8 0 f02f8f3d Feb 18 ? ?
8 S 0 root 1065 3059 0 40 20 f5f6da68 1619 feabaa2d6 Feb 18 ? 6h
8 S 0 root 88 1 0 40 20 f5b6dd706 377 f5b6926f6 Feb 18 ? C
8 S 0 root 478 1 0 41 20 f58bacbc 388 f55b1d2d6 Feb 18 ? Q
8 S 0 root 94 1 0 41 20 f5b6da808 522 f5b63de4c Feb 18 ? D
8 S 0 root 150 1 0 41 20 f5d6da110 808 f5b56500c Feb 18 ? D
8 S 0 root 96 1 0 47 20 f5d6281d 515 f5b584d2e Feb 18 ? V
8 S 0 root 144 1 0 41 20 f5d6da610 2694 ffe8f5361 Feb 18 ? 5d
8 S 0 root 1010 1 0 47 67 f5f6481d0 436 f54bec21c Feb 18 ? S
8 S 0 root 306 1 0 41 20 f5d641310 485 f5b5a6e96 Feb 18 ? N
8 S 0 root 176 1 0 51 20 f5b68ed8 446 f55b1ceb8 Feb 18 ? N
8 S 0 root 136 1 0 53 20 f5d636110 740 f5b958a62 Feb 18 ? D
8 S 0 root 129 1 0 56 20 f5d635110 447 f5b56b231 Feb 18 ? D
R daemon 110 1 0 41 20 f5d635110 584 f5b56997f Feb 18 ? D
R S 0 root 14798 1 0 45 20 f5b5ec50a 616 f5b5c7330 Feb 18 ? D
R S 0 root 129 1 0 51 20 f5e18814 507 f5b596f6c Feb 18 ? D
R S 0 root 137 1 0 63 20 f5e15688 542 f59d051440 Mar 09 ? D
B S 0 root 196 1 0 41 20 f5e146510 429 f596246f6 Feb 18 ? C
B S 0 root 213 1 0 41 20 f5e164316 584 f5b6a2b2e Feb 18 ? C
R S 0 root 199 196 0 41 20 f5e16c18 451 f5b63f816 Feb 18 ? 4d
R S 0 root 219 1 0 41 20 f5e17318 658 f5b59d686 Feb 18 ? M
```
