In addition to spilling the standard labels on your system, the glabel(8) command lets you configure GEOM labels. A GEOM label is specific to FreeBSD’s GEOM infrastructure and appears in /dev/label. Use GEOM labels with the glabel label command. Here, I apply the GEOM label root to the GPT partition da0p1:

```
# glabel label da0p1 root
```

There’s also a glabel create command, but those labels disappear at system reboot.

# ## GEOM Withering

A provider can have multiple labels. One partition might have a label based on the disk ID of the underlying storage device (/dev/diskid/somethinglong), a GPT ID (/dev/gptid/somethingevenlonger), a manually assigned label (/dev/gpt/swap0), and a device node based on the underlying device’s attachment point (/dev/ada0p1). While any number of processes can look at a disk device simultaneously, many disk operations—such as mounting a partition—require exclusive, dedicated control of the device.

To prevent accessing geoms by multiple names, when you access a device by one label, the kernel removes the unused labels. This is called withering. If I, say, mount a swap partition using the GPT label /dev/gpt/swap0, all the other labels for that partition disappear from /dev. Anyone who tries to access the corresponding /dev/gptid partition will find that the device node is missing.

Once all exclusive locks on a device are removed, the kernel de-withers the other device labels. If I deactivate that swap space, the GPT ID and raw device name reappear.

# ## The gpart(8) Command

Like many operating systems, FreeBSD once had specific partitioning tools for each partitioning scheme. Today, all disk partitioning functions,