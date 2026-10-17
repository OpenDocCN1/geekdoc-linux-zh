
```
paul@laike:-$ ls /proc
2339 4724 5418 6568 6701 7201 10175 4727 5421 6569 6996 7204 cpuinfo 1021 2873 4761 5658 6996 crypto 1023 2975 4873 5661 6328 typeinfo 141 2975 4874 5665 6652 partitions 15045 2972 4878 5927 6719 disks 15197 4980 5359 6126 6713 dm 15521 4828 5083 6032 6737 sched_debug 15554 3069 5143 6035 6755 driver 15527 5023 6228 6794 7266 self 15619 3147 5414 6418 6816 slabinfo 18108 3507 5203 6918 7282 filesystems 18191 5209 5418 6591 6968 stat 18203 3193 6228 6496 7319 swq-trigger 18896 3246 5272 6421 7157 sys 19799 3248 5921 6422 7163 iomem 19804 3213 5394 6161 7123 time_list 19830 5326 6472 7115 7529 irq 19987 5379 6426 6818 7986 uptime 19942 5370 6425 7175 7529 version 20485 5462 6450 7191 7808 version_signature 2221 5414 6551 7192 8392 vmcore 23704 5416 6568 7199 7938 locks
```

`/proc` 内部的文件属性是什么？查看当前日期和时间将显示不断更新的文件（内核的视图）。

```
root@RHELu4:-$ date
Mon Jan 29 18:06:32 EST 2007
root@RHELu4:-$ ls -al /proc/cpuinfo
-r-r--r-- 1 root 0 root Jan 29 18:06:18 /proc/cpuinfo
root@RHELu4:-$ ... time passes...
root@RHELu4:-$ date
Mon Jan 29 18:10:00 EST 2007
root@RHELu4:-$ ls -al /proc/cpuinfo
-r-r--r-- 1 root 0 root Jan 29 18:10:00 /proc/cpuinfo
```

`/proc` 中的大多数文件都是 0 字节，但它们包含了大量数据。你可以通过 `cat` `/proc/cpuinfo` 等文件看到这一点，它包含了关于 CPU 的信息。

```
root@RHELu4:-$ file /proc/cpuinfo
/proc/cpuinfo: empty
root@RHELu4:-$ cat /proc/cpuinfo
processor
  : 0
vendor_id
  : AuthenticAMD
cpu family
  : 15
model
  : 43
model name : AMD Athlon(tm) 64 X2 Core Processor 4600+
stepping : 1
cpu MHz : 2398.628
cache size : 512 KB
fdiv_bug : no
hlt_bug : no
f00_bug : no
coma_bug : no
fpu : yes
fpu_exception : yes
cpuid level : 1
wp : yes
flags : fpu vme pse tsc mser cx8 apric mtrr ge...
bogomips : 4803.54
```

为了好玩，这是 Sun Blade 1000 上的 `/proc/cpuinfo`……

```
paulspasha:~$ cat /proc/cpuinfo
cpu : TI UltraSparc III (Cheetah)
fpu : UltraSparc III integrated FPU
promblib : Version 3 Revision 2
prom : 4.2.2
type : nudu4
ccpus probed : 2
ccpus active : 2
Cpu0Bogo : 498.68
Cpu0ClkTck : 000000002cb41780
Cpu1Bogo : 498.68
Cpu1ClkTck : 000000002cb41780
MMU Type : Cheetah
State : 
CPU0 : online
CPU1 : online
```

# /proc/interrupts

在 x86 ELV 架构上，`/proc/interrupts` 显示中断信息。

```
paul@RHELv4u~$ cat /proc/interrupts
CPU
0:      13876877    IO-APIC-edge      timer
1:      15              IO-APIC-edge      i8042
8:      1               IO-APIC-edge      rtc
9:      0               IO-APIC-level    acpi
12:     67              IO-APIC-edge      i8042
14:     128             IO-APIC-edge      ideo
15:     124320          IO-APIC-edge      idel
169:    111993          IO-APIC-level    ioc0
177:    2428            IO-APIC-level    eth0
NMI:                               0
LOC:    13878037
ERR:                               0
MIS:                               0
```

在带有两个 CPU 的机器上，该文件看起来如下：

```
paul@laika:~$ cat /proc/interrupts
CPU             CPU1
0:      860013          IO-APIC-edge      timer
1:      4533            IO-APIC-edge      i8042
7:      0               IO-APIC-edge      parport0
8:      6588227         IO-APIC-edge      rtc
10:     2314            IO-APIC-fastei   acpi
12:     133             IO-APIC-edge      i8042
14:     0               IO-APIC-edge      libata
15:     72269           IO-APIC-edge      libata
18:     1               IO-APIC-fastei   yenta
19:     115036          IO-APIC-fastei   eth0
20:     126871          IO-APIC-fastei   libata,ohci3194
21:     302004          IO-APIC-fastei   ehci_hcd:usb1, uhci_hcd:usb2
22:     13334           IO-APIC-fastei   saa7133[0], saa7133[0]
24:     2347319         IO-APIC-fastei   nvidia
NMI:                72              42
LOC:    860000          859994
ERR:
```

# /proc/kcore

物理内存在 `/proc/kcore` 中表示。不要尝试用 `cat` 这个文件，而应使用调试器。`/proc/kcore` 等同于你的物理内存，外加四个字节。

```
paul@laika:~$ ls -lh /proc/kcore
-r-------- 1 root 2.0G 2007-01-30 08:57 /proc/kcore
paul@laika:~$
```

## 11.7.3. /sys Linux 2.6 热插拔
