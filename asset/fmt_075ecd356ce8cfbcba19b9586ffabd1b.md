
`cd /proc`

`ls`

要查看监控和文件系统统计的性能信息，如图 12-29 和 12-30 所示，输入以下命令：

```
cd /proc
cat stat
cat mounts
```

要查看磁盘统计的性能信息，如图 12-31 所示，输入以下命令：

```
cd /proc
cat diskstats
```

| 文件 | 编辑 | 查看 | 搜索 | 终端 | 帮助 | | | | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||
| 118 | 144 | 172 | 195 | 233 | 265 | 2028 | 2939 | 3 | 521 | 7 | 676 | buddyinfo sched debug |
| 119 | 145 | 173 | 196 | 234 | 266 | 2673 | 2984 | 30 | 522 | 78 | 688 | bus scsi |
| 120 | 146 | 174 | 197 | 235 | 267 | 2674 | 2995 | 31 | 523 | 79 | 689 | cygroups slabinfo |
| 121 | 147 | 175 | 198 | 236 | 268 | 2681 | 2996 | 32 | 524 | 80 | 690 | console softtings |
| 122 | 148 | 176 | 199 | 237 | 269 | 2682 | 2997 | 33 | 525 | 81 | 691 | conio stats |
| 123 | 149 | 177 | 200 | 238 | 270 | 2683 | 2998 | 34 | 526 | 82 | 692 | crypto mem |
| 124 | 150 | 178 | 201 | 239 | 271 | 2684 | 2999 | 35 | 527 | 83 | 693 | diskstats sysrq-trigger |
| 125 | 151 | 179 | 202 | 240 | 272 | 2685 | 3000 | 36 | 528 | 84 | 694 | diskstats sys |
| 126 | 152 | 180 | 203 | 241 | 273 | 2686 | 3001 | 37 | 529 | 85 | 695 | driver uptime |
| 127 | 153 | 181 | 204 | 242 | 274 | 2687 | 3002 | 38 | 530 | 86 | 696 | execs timer |
| 128 | 154 | 182 | 205 | 243 | 275 | 2688 | 3003 | 39 | 531 | 87 | 697 | fd timer_list |
| 129 | 155 | 183 | 206 | 244 | 276 | 2689 | 3004 | 40 | 532 | 88 | 698 | files |
| 130 | 156 | 184 | 207 | 245 | 277 | 2690 | 3005 | 41 | 533 | 89 | 699 | filesystems |
| 131 | 157 | 185 | 208 | 246 | 278 | 2691 | 3006 | 42 | 534 | 90 | 700 | zoneinfo |
| 132 | 158 | 186 | 209 | 247 | 279 | 2692 | 3007 | 43 | 535 | 91 | 701 | iomon |
| 133 | 159 | 187 | 210 | 248 | 280 | 2693 | 3008 | 44 | 536 | 92 | 702 | vmstat |
| 134 | 160 | 188 | 211 | 249 | 281 | 2694 | 3009 | 45 | 537 | 93 | 703 | keycells |
| 135 | 161 | 189 | 212 | 250 | 282 | 2695 | 3010 | 46 | 538 | 94 | 704 | kcore |
| 136 | 162 | 190 | 213 | 251 | 283 | 2696 | 3011 | 47 | 539 | 95 | 705 | keys |
| 137 | 163 | 191 | 214 | 252 | 284 | 2697 | 3012 | 48 | 540 | 96 | 706 | key-users |

图 12-28 `/proc` 目录内容

源: CentOS 7/终端

## 监控性能

```
文件 编辑 搜索 终端 帮助

User0@CentOS7:/proc

[User0@CentOS7 proc]$ cat stat

cpu 54888 75 29910 220837 653 0 370 0 0 0

cpu6 54888 75 29916 220837 653 0 370 0 0 0

intr 3074333 151 501 0 0 0 0 1 0 0 0 17231 0 0 23094 7789 76411 204 29826 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 2989 0 0 0 0 0 0 0 0 0 0 0 0 0

 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
```

要查看交换文件统计、平均负载和输入/输出内存率的性能信息，如图 12-32 所示，输入以下命令：

```
/proc
cat swaps
cat loadavg
cat iotem
```

## 第12 章 操作系统管理

```
User01@CentOS7:/proc

[User01@CentOS7:/proc] cat mounts

roots / rwfs 0

sysys /sys sysfs rw,aclabel,nosuid,nodeveec,relative 0

proc /proc rw,nosuid,nodeveec,relative 0

devpts /dev/pts devptsfs rw,aclabel,nosuid,nodeveec,size=48536k,nr_inodes=121322,mode=755 0 0

security /sys/security securityfs rw,nosuid,nodeveec,relative 0

timefs /tmp tmpfs rw,aclabel,nosuid,nodeveec,relative 0

devpts /dev/pts rw,aclabel,nosuid,nodeveec,relative,gid=5,mode=620,ptmxode=088 0 0

tmpfs /run tmpfs rw,aclabel,nosuid,nodeveec,mode=755 0 0

group /sys/group groupfs rw,nosuid,nodeveec,relative,xattr,relative_agent=usr/lib/systemd/groups-agent-name=0

group /sys/group relative 0

pstore /sys/pstore pstorefs rw,nosuid,nodeveec,relative,ccpuact,ccct 0 0

group /sys/group/blkio blkiofs rw,nosuid,nodeveec,relative,blkiot 0 0

group /sys/group/cpu cpugroupfs rw,nosuid,nodeveec,relative,cpu 0

group /sys/group/devices devicesfs rw,nosuid,nodeveec,relative,devices 0 0

group /sys/group/memory memorygroupfs rw,nosuid,nodeveec,relative,memory 0

group /sys/group/cuset cusetgroupfs rw,nosuid,nodeveec,relative,cuset 0

group /sys/group/perf_event perf_eventgroupfs rw,nosuid,nodeveec,relative,perf_event 0
```
