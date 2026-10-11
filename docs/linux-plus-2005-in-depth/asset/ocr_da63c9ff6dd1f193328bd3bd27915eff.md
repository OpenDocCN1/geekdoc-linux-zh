To extract the full backup shown in the preceding output, you can specify the `-r` option to the `restore` command followed by the archive information. In addition, you can specify the `-v` option to list the filenames restored, as shown in the following example:

```
[root@server1 root]# `restore -vrf /dev/st0`

Verify tape and initialize maps

Input is from file/pipe

Input block size is 32

Dump date: Sat Jul 23 16:43:09 2005

Dumped from: the epoch

Level 0 dump of /boot on localhost.localdomain:/dev/hda2

Label: /boot

Begin level 0 restore

Initialize symbol table.

Extract directories from tape

Calculate extraction list.

restore: ../lost+found: File exists

restore: ../grub: File exists

Extract new leaves.

Check pointing the restore

extract file ./.boot.b

extract file ./.chain.b

extract file ./.config-2.6.5-1.358

extract file ./.initrd-2.6.5-1.358.img

extract file ./.mtemtest86+-1.11

extract file ./.os2_d.b

extract file ./.System.map-2.6.5-1.358

extract file ./.vmlinuz-2.6.5-1.358

extract file ./.grub/grub.conf

extract file ./.grub/splash.xpm.gz

extract file ./.grub/menu.lst

extract file ./.grub/device.map

extract file ./.grub/stage1

extract file ./.grub/stage2

extract file ./.grub/e2fs_stage1_5

extract file ./.grub/fat_stage1_5

extract file ./.grub/ffs_stage1_5

extract file ./.grub/reiserfs_stage1_5

extract file ./.grub/vstafs_stage1_5

extract file ./.grub/xfs_stage1_5

Add links

Set directory mode, owner, and times.

Check the symbol table.

Check pointing the restore

[root@server1 root]# `_
```