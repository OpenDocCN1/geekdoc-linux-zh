
Linux box will need to be able to reach your other computers via TCP/IP. (Note that LAN is not a technical term, but I vote that it should be. Many homes are starting to have multiple computers wired together.)

## Network Access Configuration

The Network Access Configuration area allows you to configure your Ethernet card and to enter router information.

It provides two options:

- Configure Network Card
- Enter Router

Information about your network should be added or modified using this component.

## General Network Services Configuration

The General Network Services area allows you to configure your network cards, basic network services like DNS, NIS, and email.

It has three subareas:

- **Configure Domain Name Service:** This area allows you to define your DNS server.
- **Configure NIS:** This allows you to configure your workstation to use NIS (Network Information Services) as a client or as a server.
- **Select a Mail Transfer Agent:** This area allows you to configure your preferred mail transfer agent. Currently it only provides one option: sendmail.

## Boot Manager Configuration

This area displays information about lilo (the Linux Loader). On systems with multiple partitions, this will allow you to configure the boot partition and other settings. You will learn about lilo in Chapter 24.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

Search this book:

## Chapter 22
System Monitoring: Keeping an Eye on Your System

## In This Chapter

- Monitoring Memory
- Monitoring Processes
- Monitoring Your Disk
- Log Files

Many processes run on your system. In this chapter, you will get an overview on how you can monitor and control what your system is doing. For the most part, you won’t need to use any of these commands unless you suspect a problem or are trying to figure out how to fine-tune your system. Nevertheless, it’s very cool to know that you can look at different things to determine problems with performance or security, or just to keep an eye on what’s going on.

In terms of performance, Linux is fairly lean and mean as far as operating systems (OSs) go. In fact, it puts many other expensive OSs to shame. Although additional CPU speed will no doubt make your computer faster, additional RAM is likely to make more of an impact in terms of how fast you think things are happening. The single thing that can slow your computer the most is not having enough RAM for the programs you typically run at the same time. Linux makes do when it doesn’t have enough RAM by swapping.

Swapping copies data and programs currently in your computer’s memory (RAM) to disk is known as virtual memory. This makes room in the computer’s real memory (RAM) for another process to do whatever it needs to. When the swapped task needs to execute again, the Linux kernel puts it back in RAM, swapping out some other process. The amount of processes and tasks you can run depends on the amount of space you have assigned to your swap disk (virtual memory) and the amount of RAM you have installed. It is possible for you to run out of space on your swap disk, and at such a point, some programs will stop working. As you can tell, swapping doesn’t sound like something you want happening on your computer. Swapping can slow your computer to a crawl; you can tell when this is happening if you hear your hard disk thrashing (making noise all the time). The more RAM you have on your computer, the more programs you can run at the same time without swapping.

## Monitoring Memory

There are several programs that can tell you what is going on with your computer’s memory.

### How Much Memory: free

The simplest of these programs is called free. It displays how much memory you have available both in real RAM and as virtual memory, as in the following code:

```
[alberto@digital alberto]$ free
              total       used       free     shared    buffers     cached
Mem:         38956     10196     28760      8468        836      5292
-/+ buffers/cache:          4068     34888
Swap:        39276          0     39276
```

### Procinfo

Procinfo displays similar information as free, plus a bunch more. Information displayed by procinfo is collected by the kernel in the /proc directory. Here’s a screen dump of what is displayed by my lightly loaded Linux laptop:

```
[alberto@digital alberto]$ procinfo
Linux 2.0.33 (root@buildmeister.caldera.com) (gcc 2.7.2.3) #1  [digital]

Memory:     Total      Used      Free    Shared    Buffers    Cached
Mem:        38956     10316     28640      8540        836      5356

Swap:       39276         0     39276
Bootup: Sat Oct 03 09:46:52 1998 Load average: 0.00 0.01 0.00 2/32  544

user  :      0:00:07.88   0.2%  page in : 5623   disk 1: 1563r 633w
nice  :      0:00:00.00   0.0%  page out:    787
system:      0:00:11.74   0.2%  swap in :        1
idle  :      1:23:49.60  99.6%  swap out:       0
uptime:      1:24:09.21          context :    31137

irq  0:     504922 timer                 irq  8:          0
irq  1:         2 keyboard               irq  9:          1
irq  2:         0 cascade [4]            irq 10:          1
irq  3:      1872 smc91c92_cs            irq 11:      1 182365
irq  4:         1                        irq 12:          0
irq  5:         1                        irq 13:          1  math error
irq  6:         2                        irq 14:     12829 ide0+
irq  7:         1                        irq 15:          0
```

In addition to your current memory usage, it tells you when your system was last booted and its load average for the last 1, 5, and 15 minutes (0.00, 0.01, and 0.00). This information is followed by the number of runnable processes (2/32 on the listing), and the last process to run (544).

Next, procinfo displays information about the time the system has spent in user code, system code, or idle. Nice time is user code that is running with a lower priority. It also gives you the total time the machine has been up.

The next column displays information about virtual memory and disk activity. Page in and page out indicate amount of data that has moved in or out of a disk and into memory. One page is equal to 1K of data. Swap in and swap out indicate the number of pages swapped from disk to memory and from memory to disk. Context, as you can see in the preceding screen dump, is the number of context switches that have taken place. The disk column (it display more disks if you have more than one) will show the number of reads (1564r) and the number of writes (633w) since the system was booted.

## Complete Idiot's Guide to Linux:System Monitoring: Keeping an Eye on Your System

This is followed by information on activity of devices connected to IRQ, such as keyboard or serial ports.
`Procinfo` should also be able to display additional information on modules (kernel packages that are not loaded until needed) and activity for other devices if you supply the `-a` flag. At the time this book was written, the version of `procinfo` shipped with COL 1.3 was broken and didn’t display this information.

Previous Table of Contents Next

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Monitoring Processes

Your system is continuously running processes. To get an idea of what is going on with your system, there are a number of programs that you can use.

### Listing the Current Top Processes: top

Top gives you a real-time look into what your computer is doing. After you start it up, it will refresh once per second, displaying information about the principal processes on the computer.

Here’s a sample screen:

```
20:33:53 up  2:05,  2 users,  load average: 0.17, 0.07, 0.02
35 processes: 34 sleeping, 1 running, 0 zombie, 0 stopped
CPU states: 4.6% user,  6.3% system, 0.0% nice, 88.6% idle
Mem:  38956K av, 12376K used, 26580K free, 10640K shrd, 1156K buff
Swap: 39276K av,     0K used,  39276K free       5908K cached

PID USER      PRI  NI  SIZE  RSS SHARE STAT LIB %CPU %MEM   TIME COMMAND
655 alberto   20   0   612  612  452 S    0  9.7  1.5   0:10 top
656 root       8   0   592  592  436 R    0  1.7  1.5   0:00 top
1   root       0   0   340  340  268 S    0  0.0  0.8   0:02 init
2   root       0   0     0    0    0 SW   0  0.0  0.0   0:00 kflushd
3   root     -12 -12    0    0    0 SW<  0  0.0  0.0   0:00 kswapd
444 alberto    0   0   696  696  404 S    0  0.0  1.7   0:00 login
363 root       0   0   344  344  272 S    0  0.0  0.8   0:00 getty
177 root       0   0   304  304  240 S    0  0.0  0.7   0:00 rpc.rstatd
19  root       0   0     0    0    0 SW   0  0.0  0.0   0:00 nfsiod
20  root       0   0     0    0    0 SW   0  0.0  0.0   0:00 nfsiod
21  root       0   0     0    0    0 SW   0  0.0  0.0   0:00 nfsiod
22  root       0   0     0    0    0 SW   0  0.0  0.0   0:00 nfsiod
107 root       0   0   328  328  260 S    0  0.0  0.8   0:00 inetd
57  root       0   0   260  260  208 S    0  0.0  0.6   0:00 update
109 bin        0   0   312  312  244 S    0  0.0  0.8   0:00 rpc.portmap
116 root       0   0   356  356  276 S    0  0.0  0.9   0:00 syslogd
```
