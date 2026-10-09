```
What server would you like to backup? loki
Backing up loki
Backup another server? (y/n) n
$
```

# Sum All the Numbers in a given Column of a Text

```
$ awk '{ sum += $1 } END { print sum }' file
$ cat file| awk'{ sum += $1 } END { print sum }'
```

Awk can be used to tally up a column of values. You can use this trick to add up all the disk space used across all the file systems on a given system, for example.

```
$ df -mt ext4

Filesystem 1M-blocks Used Available Use% Mounted on
/dev/sda2  28215 3285       24644 12% /
/dev/sda1    485   55          406 12% /boot
$ df -mt ext4 | awk '{ sum += $3 } END {print sum}'
3340
$ sudo dmidecode --type memory

Size: No Module Installed
Size: 4096 MB

Size: No Module Installed
Size: 4096 MB
$ sudo dmidecode --type memory | grep 'Size:' | awk '{sum+=$2} END {print sum}'
8192
$
```