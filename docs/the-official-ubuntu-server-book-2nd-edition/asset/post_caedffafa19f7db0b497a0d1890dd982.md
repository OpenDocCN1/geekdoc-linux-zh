
```
/dev/md2      /boot  ext4    defaults    0    0
#/dev/md1      none   swap    sw          0    0
/dev/md4       none   swap    sw          0    0
/dev/scd0      /media/cdrom0  udf,iso9660  user,noauto,exec,utf8  0  0
/dev/fd0       /media/floppy0  auto  rw,user,noauto,exec,utf8  0  0
```

Even if you don’t use UUIDs in the fstab file, be sure to jot down the new UUID for md3 and md2. Now you are ready to reboot into the new system. Type exit in the shell you are in, and then select the “Reboot the system” option. When the system reboots and you see GRUB initially load, hit the Shift key to stop GRUB from booting so you can edit the boot options. Once you can see the list of boot choices, make sure the first option, which should be your main kernel, is highlighted, and then hit E to edit it. One of the lines will say set root=‘(md0)’, or if not, it will point to your old root device, so change it to point to the new device. In my case I change it to set root=‘(md3)’. Next there are two different lines that list the UUID for your original root partition. Change the UUID in the line that begins with search to the UUID of your new /boot partition (/dev/md2 in the example). That tells grub2 where to search for its files. Change the UUID in the line that begins with linux to the UUID of the new root device (/dev/md3). Also, since your boot partition is separate from the root partition, you will need to remove the /boot from any lines that reference it, because the initrd and kernel files will be within the main /boot directory. In my case the final GRUB options read

```
recordfail
insmod raid
insmod mdraid
insmod ext2
set root='(md2)'
search --no-floppy --fs-uuid --set 5452717c-727c-4ba9-8a75-4ac362f0lee6
linux /vmlinuz-2.6.32-19-generic-pae
root=UUID=2bfc0697-f109-4986-83a5-1f7c162e37bf ro quiet splash
initrd /initrd.img-2.6.32-19-generic-pae
```

Once you are finished changing these options, hit Ctrl-X to boot into the system on the RAID array. If you set the boot arguments and the /etc/fstab correctly, when you boot and type df you should see that your root partition is /dev/md3 (or what you assigned your RAID array) along with your /boot partition:

```
$ df
Filesystem     1K-blocks      Used Available Use% Mounted on
/dev/md3       16254420    638276   14796844  5% /
... 
/dev/md2        101018     23974     71828  26% /boot
```

When you check /proc/mdstat, you will see your active arrays running on a single disk:

```
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6]
[raid5] [raid4] [raid10]
md4 : active raid5 sdc5[1] sdb5[0]
  176512 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU_]
md3 : active raid5 sdc2[1] sdb1[0]
  16386048 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU_]
md2 : active raid1 sdc1[1] sdb1[0]
  104320 blocks [2/2] [UU]
md1 : active raid1 sda5[0]
  88256 blocks [2/1] [_U]
md0 : active raid1 sda1[0]
  8297472 blocks [2/1] [_U]
unused devices: <none>
```

It’s possible that md0 and md1 will not show up when you check /proc/mdstat. In that case, you won’t need to destroy those arrays. Otherwise you must destroy the original RAID arrays /dev/md0 and /dev/md1 so we can repartition the drive and assign those new partitions the new arrays:

```
$ sudo mdadm --stop /dev/md0
mdadm: stopped /dev/md0
$ sudo mdadm --stop /dev/md1
mdadm: stopped /dev/md1
```

Once you are ready to repartition the original drive, you can check /proc/mdstat and see that those arrays are no longer available:

```
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6]
[raid5] [raid4] [raid10]
md4 : active raid5 sdb5[0]
176512 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU_]

md3 : active raid5 sdc2[1] sdb1[0]
16386048 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU_]

md2 : active raid1 sdc1[1] sdb1[0]
104320 blocks [3/2] [UU_]

unused devices: <none>
```

Now repartition /dev/sda as you did /dev/sdb so its partitions match the other two drives. Remember to set the partition types to fd. Once you save your changes, if fdisk complains that the kernel is going to use the old partition table, you have a small problem. You won’t be able to safely add the new /dev/sda partitions to your RAID at this point. Instead, boot back into the rescue disc, select your RAID 5 root file system, then choose “Execute a shell in /dev/md3” (or the name of your root file system). Once you are at a prompt, type mount /boot so that the /boot partition is available. Otherwise, if fdisk doesn’t give that complaint, proceed with the next steps.

Finally, you are ready to add the original partitions to each array:

```
$ sudo mdadm /dev/md2 --add /dev/sda1
$ sudo mdadm /dev/md3 --add /dev/sda2
$ sudo mdadm /dev/md4 --add /dev/sda5
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6]
[raid5] [raid4] [raid10]
md4 : active raid5 sda5[3] sdc5[1] sdb5[0]
176512 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU_]
resync=DELAYED

md3 : active raid5 sda5[3] sdc2[1] sdb1[0]
16386048 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU_]
[=>.................] recovery = 5.6% (471936/8297472)
finish=12.3min speed=10550K/sec

md2 : active raid1 sda1[2] sdc1[1] sdb1[0]
104320 blocks [3/3] [UUU]

unused devices: <none>
```
