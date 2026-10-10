```
md1 : active raid1 sda6[1] hda5[0] 256896 blocks [2/2] [UU] resync=89%
finish=0.0min
unused devices: <none>
```

As you can see, a resync is in progress, and should be finished any second. After the resync is complete, catting /proc/mdstat will display something like this:

```
Personalities : [linear] [raid0] [raid1]
read head 1024 sectors
md1 : active raid1 sda6[1] hda5[0] 256896 blocks [2/2] [UU]
unused devices: <none>
```

The mirror is now sync’d up. Note that it’s perfectly safe to start using a mirror even when the syncing process is underway; drive IO will be slightly slower, but not significantly slow, as the kernel paces itself during the resync process so that mirror IO performance does not suffer. Now that you have your RAID 1 volume created, mount it and play around with it. Notice that writes are slightly slower and reads are slightly faster.

The Software RAID 1 implementation under Linux is incredibly flexible and robust. One major benefit of using RAID 1 is that it is easy to turn off in an emergency situation. For example, say that one of the hard drives in your mirror fails, and it is past warranty. You’re broke, and you don’t have any money to purchase a replacement drive. Turning off a RAID 1 mirror is as easy as:

```
> umount /mnt/raid
> raidstop /dev/md0
```

Then, assuming that /dev/hda3 is the RAID 1 partition that is on your working drive, change all references to /dev/md0 to /dev/hda3 in your /etc/fstab. Because each mirror contains a valid ext2 file system in its own right, you can continue normal operation of your machine in non-mirrored mode:

```
> mount /dev/hda3 /dev/raid
```

The system can now be powered down and the defective drive can be thrown away! This trick only works with RAID 1; it will not work with RAID 0, 4, 5 or Linear mode.

You should now have a good overview of the Linux kernel’s flexible Software RAID abilities. If you are interested in setting up a RAID 4 or 5 volume or a Linear volume, look at the following man pages:

```
> man mdraid
> man raidtab
```

They should give you all the information you need. Unfortunately, most of the Web-based information (including the Software-RAID HOWTO) is seriously out-of-date, and differ from the steps required to get a modern Software RAID setup working under Linux. Keeping this in mind, you might want to look at