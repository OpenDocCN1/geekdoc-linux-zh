Display pressing key 2:

```
top - 13:45:45 up 74 days, 7:01, 2 users, load average: 0,00, 0,02, 0,04
Tasks: 467 total, 1 running, 465 sleeping, 1 stopped, 0 zombie
%Cpu(s): 0,0 us, 0,2 sy, 0,0 ni, 99,8 id, 0,0 wa, 0,0 hi, 0,0 si, 0,0 st
%Cpu0: 0,0 us, 0,0 sy, 0,0 ni, 99,9 id, 0,0 wa, 0,0 hi, 0,0 si, 0,0 st
%Node1: 0,0 us, 0,5 sy, 0,0 ni, 99,5 id, 0,0 wa, 0,0 hi, 0,0 si, 0,0 st
```

Figure 6.10: Top command output header example

# ## Commands atop and htop

These commands are a modern alternative to the traditional top. Figure 6.11 shows the aspect of the application atop, which includes more information related to the system:

ATOP - server 2022/08/13 13:55:33 -- -zombie---- 10s elapsed
PRC sys 1.10s user 0.12s #proc 473 #zombie 0 no proccct
CPU sys 7% user 1% irq 1% idle 3193% wait 0%
CPU avg1 0.06 avg5 0.11 avg15 0.09 csw 9950 intr 7455
MEM tot 251.5G free 22.6G buff 1.0M slab 7.8G numode 2
SWP tot 0.0M free 0.0M swcac 0.0M vmcom 313.3G vmlim 125.8G
PAG numamig 0 migrate 543 swim 0 swout 0 oomkll 0
DSK transport sda busy 0% read 0 write 7 avio 0.14 ms
NET transpot tccpi 5 tcpc 5 udpi 0 udpo 0
NET network xpl 29 xpo 7 ipfrw 0 deliv 6
NET eth1 0% pcki 72 pcko 6 si 4 Kbps so 1 Kbps
NET eth2 0% pcki 68 pcko 0 si 3 Kbps so 0 Kbps

PID SYSCPU USRCPU RDELAY VGROW RGROW RDGSK WRDSK CPU CMD 1/4
247 0.99s 0.00s 0.00s 0B 0B 0B 0B 16% ksmd
83078 0.02s 0.10s 0.00s 0B 0B 0B 0B 1% qemu-kvm
2120339 0.03s 0.01s 0.00s 0B 0B 0B 0B 0% atop
36944 0.00s 0.01s 0.00s 0B 0B 0B 0B 0% vbvncd
1531 0.01s 0.00s 0.00s 0B 0B 0B 0B 0% NetworkManager
248 0.01s 0.00s 0.00s 0B 0B 0B 0B 0% khugepaged
83095 0.01s 0.00s 0.00s 0B 0B 0B 0B 0% vhост-83078
91418 0.01s 0.00s 0.00s 0B 0B 0B 0B 0% kvm-pit/91396
281928 0.01s 0.00s 0.00s 0B 0B 0B 0B 0% kvm-pit/281867
2115603 0.01s 0.00s 0.00s 0B 0B 0B 0B 0% kworker/0:2-ev

Figure 6.11: Example aspect of command atop

Figure 6.12 shows the aspect of the htop application, which have between overview of the CPU usage: