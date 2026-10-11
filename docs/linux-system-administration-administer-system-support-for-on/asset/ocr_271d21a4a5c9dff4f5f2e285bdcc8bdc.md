This means that it's using the primary disk on the first IDE controller. If you type **m**, you will get a list of choices, as follows:

```
Command action
a toggle a bootable flag
b edit bsd disklabel
c toggle the dos compatibility flag
d delete a partition
l list known partition types
m print this menu
n add a new partition
p print the partition table
q quit without saving changes
t change a partition's system id
u change display/entry units
v verify the partition table
w write table to disk and exit
x extra functionality (experts only)

Command (m for help):
```

**What we want to do is add a new partition. To add it, type n.**

```
Command (m for help): n
Command action
e extended
p primary partition (1-4)
```

Press p, and then pick the partition number. If you already have DOS, Windows 95, or some other operating system be sure to specify at least 2 partitions. If you don't, you get a message telling you that the only partition currently recognized is already in use. Next you'll be prompted to specify the first cylinder to use as the starting point of the new partition. For example, it might say

```
First cylinder (801-1023):
```

Tell it 801 unless you like playing games with disk space. Next you'll be prompted to designate the last cylinder of the partition, which indicates how much space you want.

```
Last cylinder or +size or +sizeM or +sizeK (801-1023):
```

It's quicker, however, simply to tell fdisk how much space you want. Let's say you want 250MB for this partition. You would then type +250M and press Return or Enter. If you have more than 250MB, enter the amount accordingly.