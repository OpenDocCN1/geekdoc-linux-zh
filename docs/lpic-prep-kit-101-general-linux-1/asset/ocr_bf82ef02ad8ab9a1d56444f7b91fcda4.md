How all this is accomplished is relatively simple. Linux moves unused pages of memory out to the swap partition, allowing more applications to run simultaneously on your system. However, swapping is slower than using physical RAM. If you have 4MB of RAM or less, you will need to have a swap partition or the installation will fail.

One possible partitioning plan is shown in Table 3.2.

| Partition | Contents |
| :--- | :--- |
| / | Contains applications and configuration files |
| /var | Contains log files |
| /usr | Contains system software |
| /tmp | Contains temp files |
| /home | Contains users' home directories |
| swap | Acts as virtual memory |


One disadvantage of multiple partitions is that you cannot enlarge a partition dynamically if it should get full. Rather, you would have to delete the partition and then re-create it with a larger size. With the larger hard drives available now, many system administrators use fewer partitions.

Plan your partitioning scheme out on paper. Although you can always blow away your partitions and start all over, having a well thought-out plan before starting the partitioning process will keep you from having to reinstall because of space constraints.

# Key Concept

An advantage of multiple partitions is that you can better control the amount of space dynamic files such as log files can consume. On the other hand, a partition cannot be dynamically enlarged if it becomes full.

# Tips

If you are installing Linux on a computer running another operating system and there is no free space to create a new partition, you can use `fips.exe` to non-destructively divide a single FAT16 partition in two.

This program does not work with any filesystem except FAT16. Although fips usually works without losing any existing data, be sure to make a complete backup of your system before using it.