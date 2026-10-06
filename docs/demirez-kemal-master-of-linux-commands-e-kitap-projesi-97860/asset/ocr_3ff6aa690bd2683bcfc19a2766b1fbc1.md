# Free

The amount of memory used can be learned by this command. If you use the **-m** parameter as **free -m** form, the out put will be more coordinated (MB).

```
root@kemal:~# free -m
total      free shared
ached Mem: 491 483 7 84
196
-/ buffers/cache: 284 206
Swap: 1912 1542
```

# Hdparm

Get information about the hard disk, **hdparm** command is used. At its most basic **hdparm <drive>** is listed with information about your disk.

```
root@kemal:~# hdparm /dev/sda
/dev/sda:
multcount = 16 (on)
I0support = 1 (32-bit)
readonly = 0 (off)
readahead = 256 (on)
geometry = 4864/255/63, sectors = 78140160, start = 0
```

For more information about disk performance **hdparm -T <drive>** command is used.

```
root@kemal:~# hdparm -T /dev/sda
/dev/sda:
Timing cached reads: 926 MB in 2.00 seconds = 462.91 MB/sec
Timing buffered disk reads: 92 MB in 3.02 seconds = 30.44 MB/sec
root@kemal:~#
```

But however, we said that **hdparm** command can also be used to get information, but the real purpose of this command is settings for the hard disk hardware features and settings