# CHAPTER 11 Other Helpful Tools

Regardless of the interactive or noninteractive is, the reported information is identical. Due to the nature of the hardware and system data PowerTOP must collect, the tool requires root privileges. The following sections describe the information reported and how it should be interpreted.

# 11.3.1 OVERVIEW

In "Performance Is Power Efficiency" section of Introduction, the concept of "race to idle" was used as a technique for improving power consumption. This concept, bursting to complete work quickly, is only applicable if the work can be completed quickly. Longer running tasks, such as daemons, should be written to the processor to take advantage of these deep sleep states.

As described in "C states" section of Chapter 3, for the processor to enter deep sleep, it must be halted, and therefore not executing instances. Each C state has an entry and exit latency, it is the job of the intel_idle driver in the Linux kernel to request the deepest C state that meets the latency requirements again. When the kernel is kicked, only waking up when needed, it is crucial that user space applications are carefully aware about how they wake the system from slumber. PowerTOP reports these occurrences in order to allow the user to identify misbehaving applications that are impacting power consumption.

Figure 11.1 shows the default window in PowerTOP, running on an idle system. After the backlight, which was on maximum, was consuming the most power. Additionally, the network devices, the wireless card and Ethernet card, are consuming a lot of power. Notice that the interrupts and interrupt handler are also causing a significant number of wakes.

| PowerTOP 2.5 | Overview | Idle state | Frequency | Device states | Tunables |
| --- | --- | --- | --- | --- | --- |
| The estimated remaining time is 7 hours, 21 minutes | | 0.1 GPa/sec, 0.0 VFS ops/sec and 0.8% CPU use | | |
| Power est. | Usage | Events/ | Category | Description | |
| 10.6 W | 86.7% | Device | Display backlight | |
| 3.54 W | 1.1 pts/s | Device | Network interface: wlp2s0 (iwlwifi) | |
| 2.41 W | 0.0 pts/s | Device | Network interface: eth0 (e1000e) | |
| 37.3 ms | 3.2 us/s | 80.0 | Process | [irq-iwlwifi] | |
| 4.87 ms | 327.7 us/s | Timer | ticked_timer | |
| 3.09 ms | 194.1 us/s | Process | [46] iwlwifi | |
| 2.49 ms | 136.8 us/s | 9.4 | Process | /user/systemd-switched | |
| 2.46 ms | 124.8 us/s | 0.0 | Process | /usr/libexec/gnome-terminal-server | |
| 1.57 ms | 115.3 us/s | 0.3 | Process | /usr/lib/systemd-background none | |
| 1.95 ms | 264.5 us/s | 0.0 | Process | [kworker/u6:5] | |
| 1.52 ms | 250.6 us/s | 0.0 | Process | /usr/libexec/deja-dup/deja-dup-moni | |
| 1.86 ms | 231.4 us/s | 0.0 | Process | [1] timer(softirq) | |

FIGURE 11.1
PowerTOP nurcurs interface overview.