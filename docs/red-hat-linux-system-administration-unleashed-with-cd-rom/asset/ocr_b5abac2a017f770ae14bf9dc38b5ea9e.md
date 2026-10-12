```
Bus 0, device 20, function 0:
Ethernet controller: DEC DC21140 (rev 34).
Medium devsel. Fast back-to-back capable. IRQ 3. Master Capable.
→Latency=32. Min Gnt=20.Max Lat=40.
I/O at 0xec80 [0xec81].
Non-prefetchable 32 bit memory at 0xffafb00 [0xffafb00].
```

If you're unable to resolve the problem, you should send a description of the problem along to the Linux hardware information maintainers. Instructions on how to file a report can be found in the Linux Hardware Compatibility HOWTO located in /usr/doc/HOWTO. You may also need to search Internet resources for the location of a more up-to-date driver for the device.

The preceding listing (for /proc/pci) provides an example of how the Linux /proc filesystem can be used as a diagnostic tool. The next section explores additional uses of /proc.

# Diagnostic Tools

Linux supplies a number of useful diagnostic tools to assist with troubleshooting. These include the /proc filesystem, isapnp, ifconfig, and network card diagnostic programs. This section looks at ways of using these tools to troubleshoot hardware problems.

# Using /proc for Diagnosis

In addition to /var/log/dmesg and /var/log/boot.log, one of the most useful diagnostic tools in Linux is the /proc filesystem, outlined in Chapter 4, “Where Do I Find...?” As you have seen in the case of PCI information, it provides information that can be useful for diagnosing system problems.

Interrupt conflicts, for instance, can prevent hardware devices from working properly. You can check the status of interrupts by inspecting /proc/interrupts. To inspect this file, type cat /proc/interrupts, as in the following listing:

```
[root@wallace /root]# cat /proc/interrupts

CPU0
0: 518188 XT-PIC timer
1: 15017 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 339652 XT-PIC eth0
4: 61197 XT-PIC serial
```