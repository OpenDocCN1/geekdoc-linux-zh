# Plug and Play support

In my personal experience, Plug and Play should really be called Plug and Pray (don't know who said it first). I urge you not to enable PNP in something so nice as Linux.

```
Plug and Play support (CONFIG_PNP) [N/y/?]
```

You should know the answer to this prompt. If you have a card that works only in PNP mode, you are likely to encounter problems. The best thing to do is buy hardware that has an option to turn off PNP.

# Block devices

In this section, you are asked about disk drives.

```
Normal PC floppy disk support (CONFIG_BLK_DEV_FD) [Y/m/n/?]
```

Because most systems have floppy drives, this should be set to yes.

```
XT hard disk support (CONFIG_BLK_DEV_XD) [N/y/m/?]
```

Modern PCs don’t use XT hard disks any more so you should choose the default answer unless you happen to have XT hard disks.

```
Compaq SMART2 support (CONFIG_BLK_CPQ_DA) [N/y/m/?] okcmpk
Compaq Smart Array 5xxx support (CONFIG_BLK_CPQ_CISS_DA) [N/y/m/?]
Mylex DAC960/DAC1100 PCI RAID Controller support (CONFIG_BLK_DEV_DAC960) [N/y/m/?]
Loopback device support (CONFIG_BLK_DEV_LOOP) [N/y/m/?] y
Network block device support (CONFIG_BLK_DEV_NBD) [N/y/m/?]
Multiple devices driver support (RAID and LVM) (CONFIG_MD) [N/y/?]
```

# Networking options

Networking is one of the most important sections. Here, you decide on various networking issues.

```
Packet socket (CONFIG_PACKET) [Y/m/n/?]
```

Applications such as tcpdump use the Packet protocol; therefore, you should accept the default answer.

```
Kernel/User netlink socket (CONFIG_NETLINK) [N/y/?]
```