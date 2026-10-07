
# Summary

Now that we have covered the Top Ten Hacking utilities, please don't think for a second that this list is comprehensive. There are dozens of open source tools available to perform these and other similar functions. What I hope I have done in this chapter is open your eyes to the potential uses of some of the most popular security tools available, and illustrate how they do what they do.

The lab work that I have done to provide the screen shots in this note were not done with magic, smoke, or mirrors. They were done by simply downloading the utility and running them against other machines in my lab. Conceptually, if you can do the same thing in your own test lab, then you can get a feel for these and other similar tools, and what kind of forensic footprint they may leave. Armed with this information, you can transfer that footprint to your current case, and hopefully draw much closer to providing your customer with an answer of what happened, when, and how.

Not all security tools that can be used for hacking were meant for that purpose. As we have seen in looking at tools like Netcat, nmap, nessus, and hping2, the majority of these tools were initially designed to help administrators secure their infrastructures. Remember, the “catch phrase” of the hacking world is “getting something to do that” when you are working your cases. The customer may tell you that “such and such” is impossible; however, as we have already discussed, just because something has never happened before, does not mean that it's impossible.

Test, test, and test. Whenever you see a tool or utility you are unfamiliar with, install it in your lab and see what it's all about. Once you you have successfully profiled that particular utility, post your results to a forensic forum. Let other investigators see what you have seen, and benefit from your research. You never know, your work may help somebody else catch the bad guy.

# Chapter 6

# The /Proc File System

Solutions in this chapter:

- Introduction
- Putting It All Together
- sysfs

# Introduction

Previous chapters have (hopefully) driven the importance of collecting volatile data. This chapter will help you collect the most volatile data present on a UNIX system—the contents of the /proc file system. You first saw /proc in Chapter 3. While some of the information available from /proc can be collected via other methods, /proc is the only place you'll be to collect incredibly vital data.

The /proc file system is what is known as a "pseudo" or "virtual" file system, non-file data represented as a hierarchical file system that doesn't actually exist on disk. It was originally designed to access information, but has since grown to encompass other core and in-memory data. /proc was originally implemented in Version 8 UNIX, while most modern UNIX trace their /proc lineage to the Plan 9 implementation. One of the benefits of the /proc file system is that it allows user identities to access information that would normally be restricted to kernel space (e.g., information about the state of memory, running processes, and active network connections). In fact, many of the utilities you use to collect data in Chapter 3, retrieve it from /proc. (See Figure 6.1.)

# Figure 6.1 The Contents of /proc on a Typical Fedora Core 8 Linux System

```
[root@localhost:/]# ls
1701 1814 2834 2727 2777 2971 2945 418
1687 1818 2836 2246 2675 2872 2972 425
1684 1893 2045 2277 2885 3042 3042 465
1160 1846 2055 2628 2879 2928 2978 425
1185 2125 2210 2382 2819 2879 2928 466
1393 2089 2131 2367 2463 2593 2693 511
1359 1918 2143 2674 2885 3042 3466 523
1390 1918 2143 2673 2762 2997 3115 531
1595 1931 2161 2306 2516 3061 3103 503
1743 1937 2180 2675 2858 3018 3189 58
1750 1961 2167 2732 2857 3023 3230 61
1755 1970 2186 2739 2857 2937 3230 62
1771 1988 2238 2744 2839 2939 381 62
1772 2232 2376 2776 2868 2944 408
[root@localhost]: _
```

# The /Proc File System

In addition to providing data about the current state of the machine, some entities allow modification. In Figure 6.1 you can see the large number of directories in /proc.

The cmdline file shows the boot parameters that were passed to the kernel:

```
cat /proc/cmdline
ro
```

This file provides data from the real time clock (rtc), which keeps time while the system is off:

```
rtc_time: 20:30:22
rtc_date: 2008-04-02
rtc_epoch: 00:00:00
alarm_enable: no
BCD: yes
square_wave: no
alarm_IRQ: no
update_IRQ: no
periodic_IRQ: no
batt_status: 1024
periodic_freq: no
```

This file contains information about all the processors on the system.

```
cpuinfo
info
```

This file lists the file systems currently supported (in one manner or another) by the kernel. Additional file system support may be available in modules that are currently inserted. Additionally, the presence of a file system in this list does not indicate whether read-write access is available. Virtual or pseudo-file systems will be preface with “NODEV,” indicating that they do not require a physical device.![](img/fd8e85097b37559dbc07dc22fd8cb1fe_163_0.png)

```
nodev sysfs
nodev rootfs
nodev bdev
nodev proc
nodev cpuset
nodev binfmt_misc
nodev debugfs
nodev securityfs
nodev sockfs
nodev usbfs
nodev pipefs
nodev anon_inodefs
nodev futexs
nodev tmpfs
nodev notifyfs
nodev devpts
nodev ramfs
nodev hugebfs
iso9660
nodev mqueue
extext3
nodev vmhgfs
nodev rpc_pipefs
nodev vmblock
nodev autofs
```

# filesystems

This is the 2.6 kernel’s replacement for “ksyms,” and provides a listing of all symbols present in the kernel. The 2.4 kernels provides only a listing of exported symbols. This information may be useful in determining if the machine you are examining has compromised with a rootkit, as some will leave telltale traces here. For example, Adore and Adore-based rootkits and the Heroin rootkit are both detectable via syscalls. It is important to note, however, that the absence of root track in this file does not necessarily mean the system is clean; it could be compromised by a better rootkit.

# kcore

kcore is a representation of the physical memory of the machine stored in “core” file format, suitable for debugging in the GNU debugger (gdb). This data is incredibly important in intrusion investigations. Analysis of this data can be as simple as
