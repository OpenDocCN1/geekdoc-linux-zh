# # Parted

To disk partition there is another tool we can use which is parted tool. To get information about disc sections you can use parted -l command.

```
root@kemal:~# parted -l
Model: ATA TOSHIBA MK4032GA (scsi)
Disk /dev/sda: 40,0GB
Sector size (logical/physical): 512B/512B
Partition Table: mdsos
Disk Flags:
Number Start End Size Type File system Flags
1 1049KB 39,0GB 39,0GB primary ext4 boot
2 39,0GB 40,0GB 1053MB extended      
5 39,0GB 40,0GB 1053MB logical linux-swap (v1)
```

When we use parted without parameters we see a prompt waiting new command. To view the Help topics, we can use the help command.

```
root@kemal:~# _nGNU Parted 3.2
Using /dev/sda
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) help
align-check TYPE N for TYPE(min|opt)
alignment print general help, or on help
(COMMAND) COMMAND
mkmable LABEL-TYPE create a new disktable (partition table)
nkpart PART-TYPE [FS-TYPE] START END
name NUMBER NAME make a partition
print [devices|free|all|NUMBER] display the partition table, or
available devices, free space, all found partitions, or a particular partition
quit exit program
rescue START [END] rescue a lost partition near START and END
rescue recover partition NUMBER END
```

To see a list of the partitions on the help screen we can see that print command is used.

* Neither*