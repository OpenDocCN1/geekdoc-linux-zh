This is very handy when tracking your log files. For example, enter the following to continuously see the latest log messages:

```
$ tail -f /var/log/messages
```

# Killing Processes

To kill a process, use the kill command. You must know the ID of the process you want to kill; you can use ps to get it. Alternatively, you can use the killall command, which takes the name of the process you want to kill rather than its ID. For example, the following kills all the Netscape processes that belong to you:

```
$killall netscape
```

Be very careful with this command when you are running as root. You can easily kill other users' processes by mistake!

# X Window System Tips

If you use SuSE Linux as a desktop operating system, you will be using the X Window System quite often. We will discuss several tips to enhance your X Window experience in the following sections.

# Speeding Up Your X Window System

The 2.2.x kernel uses a feature present in Pentium Pro and later processors called Memory Type Range Registers. You must enable them in your kernel configuration, in the Processor Type and Features section.

Using MTRR, you can tell the kernel to enable write combining on a block of memory, which increases the speed of data transfers. This is useful if you have a PCI or AGP display card. You can enable write combining on the card's memory, thus speeding up your graphics. This in turn will speed up your X Window System quite considerably.

To use MTRR, you need to know the beginning of your card's memory address space. You can find this information by looking at the /proc/pci file:

```
# cat /proc/pci
```

The previous command gives you a list of all the PCI devices you have on your system. You are interested only in the part that has to do with your graphics card. The following is an example of such a section:

```
Bus 1, device 0, function 0:
VGA compatible controller: NVidia Unknown device (rev 21).
Vendor id=10de. Device id=2d.
Medium devsel. Fast back-to-back capable.
-IRQ 11. Master Capable. Latency=64. Min Gnt=5.Max Lat=1.
Non-prefetchable 32 bit memory at 0xf5000000 [0xf5000000].
Prefetchable 32 bit memory at 0xfc000000 [0xfc000000].
```