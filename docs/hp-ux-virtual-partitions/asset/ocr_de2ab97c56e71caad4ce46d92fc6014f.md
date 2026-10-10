```
`# dmesg`

```
Memory Information:
  MBD / - cal page size = 4096 bytes, logical page size = 4096 bytes
  Physical: 4194304 Kbytes, lockable: 3180924 Kbytes, available: 3655192 Kbytes
```
```

This listing shows a *Physical* memory of 4GBytes. You could also run GlancePlus and select the *Memory* screen.

Memory can easily be specified for a vPar with *m::size*, where *size* is in MBytes. To specify 2 GBytes in a virtual partition, you would use the option *m::2048*.

After assigning memory to vPars you’ll want to confirm that indeed each vPar has in it the amount of memory you specified. You can verify this in a variety of ways. The first is by issuing **dmesg** when booting Virtual Partitions. The Virtual Partitions Monitor boots only the devices you have specified as part of a Virtual Partition. The following example shows only the memory-related output of **dmesg** for *cable1*:

```
`Memory Information:`

```
cvhcon3:/ # page size = 4096 bytes, logical page size = 4096 bytes
  Physical: 2096128 Kbytes, lockable: 1576748 Kbytes, available: 1815620 Kbytes
```
```

Notice that this output shows 2 GBytes of RAM for *cable1*, as was specified when the *vPar cable1* was created. This is different from the example in Chapter 2, where *cable1* had one GByte of RAM. This is an indicator of how low-level vPars work, in that resources were assigned to *cable1* at the time of boot, ensuring that only the specified resources were assigned to the vPar.

We can also view memory-related information by running GlancePlus and selecting the *memory* screen. The following screen shot shows the total memory of the system when booting standard HP-UX and not Virtual Partitions as we have done in Figure 5-3: