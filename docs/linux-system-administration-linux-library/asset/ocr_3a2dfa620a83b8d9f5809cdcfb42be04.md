| anaconda | gzip | mkfs.ext2 | ps |
| badblocks | head | mknod | python |
| bash | hwclock | mkraid | python1.5 |
| cat | ifconfig | mkswap | raidstart |
| chatter | init | mlabel | raidstop |
| chmod | insmod | mmd | rcp |
| chroot | less | mmount | rlogin |
| clock | loader | move | rm |
| collage | ls | modprobe | rmod |
| cp | lsattr | mount | route |
| cpio | lsmod | mpartition | rpm |
| dd | mattrib | mrd | rsh |
| ddcprobe | mattblocks | mread | sed |
| depmode | mbadblocks | mren | sh |
| df | mcd | mshowfat | sync |
| e2fsck | mcopy | mt | tac |
| fdisk | mdel | mtools | tail |
| fsk | mdtree | mtype | tar |
| fsck.ext2 | mdir | mv | touch |
| ftp | mdu | mzip | traceroute |
| genhdlist | mformat | open | umount |
| gnome-pty-helper | minfo | pico | uncpio |
| grep | mkdir | ping | uniq |
| gunzip | mk2fs | probe | zcat |

If your root filesystem is undamaged, you can mount it and use the chroot command to run commands as if the original root filesystem were your root directory. You can mount all the partitions on this root filesystem and essentially run your own system. Under Red Hat 6.2 and beyond, you are required to create your own devices, before you can mount /dev/hda1,you'll need to use the mknod command to create /dev/hda, /dev/hda1, and /dev/hda2.

```
# mknod /dev/hda b 3 0
# mknod /dev/hdal b 3 1
```