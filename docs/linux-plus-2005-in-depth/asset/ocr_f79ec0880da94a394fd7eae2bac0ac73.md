# SYSTEM BACKUP





DUMP: 20 tape blocks (0.02MB) on 1 volume(s)
DUMP: finished in less than a second
DUMP: Date of this level 1 dump: Sat Jul 23 16:50:57 2005
DUMP: Date this dump completed: Sat Jul 23 16:50:58 2005
DUMP: Average transfer rate: 0 kB/s
DUMP: DUMP IS DONE

```
[root@server1 root]# cat /etc/dumpdates
/dev/hda2 0 Sat Jul 23 16:43:09 2005
/dev/hda1 1 Sat Jul 23 16:50:57 2005
[root@server1 root]# _
```

To view the contents of an archive, you can specify the -t option to the restore command fol-lowed by the archive information. To view the contents of the full backup performed earlier, you can place the appropriate tape into the tape drive and execute the following command:

```
[root@server1 root]# restore -tf /dev/st0
Dump   date: Sat Jul 23 16:43:09 2005
Dumped from: the epoch
Level 0 dump of /boot on localhost.localdomain:/dev/hda2
Label: /boot
  2               .
 11              ./lost+found
4033             ./. grub
4035             ./grub/grub.conf
4034             ./grub/splash.xpm.gz
4036             ./grub/menu.lst
4037             ./grub/device.map
4038             ./grub/stage1
4039             ./grub/stage2
4040             ./grub/e2fs_stage1_5
4041             ./grub/fat_stage1_5
4042             ./grub/ffs_stage1_5
4043             ./grub/reiserfs_stage1_5
4044             ./grub/vstafs_stage1_5
4045             ./grub/xfs_stage1_5
 12              ./boot.b
 13              ./chain.b
 14              ./config-2.6.5-1.358
 15              ./initrd-2.6.5-1.358.img
 17              ./memtest86+-1.11
 19              ./os2_d.b
 22              ./System.map-2.6.5-1.358
 20              ./vmlinuz-2.6.5-1.358
[root@server1 root]# _
```