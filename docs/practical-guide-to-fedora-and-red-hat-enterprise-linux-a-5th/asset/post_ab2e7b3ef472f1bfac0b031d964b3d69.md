
If you put /boot on a separate partition, it is a good idea to put it at the beginning of the drive (partition 1) so there is no issue of Linux having to boot from a partition located too far into the drive. When you can afford the disk space, it is desirable to put each major filesystem on a separate partition. Many people choose to combine / (root), /var, and /usr into a single partition, which generally results in less wasted space but can, on rare occasions, cause problems.

Although parted can create some types of filesystems, it is typically easiest to use this utility to create partitions and then use mkfs and mkswap to create filesystems on the partitions.

The following sequence of commands defines a 300-megabyte, bootable, Linux partition as partition 1 on a clean disk:

```
# parted /dev/hdb
...
Using /dev/hdb
(parted) mkpart                (create new partition)
Partition type?  primary/extended? primary     (select primary partition)
File system type?  [ext2]?            (default to an ext2 filesystem)
Start? 1                 (start at the beginning of the disk)
End? 300m               (specify a 300-megabyte partition)
(parted) help set              (use help to check the syntax of the set command)
set NUMBER FLAG STATE           change a flag on partition NUMBER
```

NUMBER is the partition number used by Linux. On msdos disk labels, the primary partitions number from 1 to 4, logical partitions from 5 onwards. FLAG is one of: boot, root, swap, hidden, raid, lvm, lba, hp-service, palo, prep, msftres. STATE is one of: on, off.

```
(parted) set 1 boot on          (turn on the boot flag on partition 1)
(parted) print              (verify that the partition is correct)
Disk geometry for /dev/hdb: 0kB - 250GB
Disk label type: msdos
Number  Start     End       Size     Type     File system  Flags
   1      1kB     300MB     300MB    primary   ext2         boot
(parted) quit
Information: Don't forget to update /etc/fstab, if necessary.
```

When you specify a size within parted, you can use a suffix of k (kilobytes), m (megabytes), or g (gigabytes). After creating a partition, give a print command to see where the partition ends. Perform this task before you define the next contiguous partition to make sure you did not waste space. After setting up all the partitions, exit from parted with a quit command.

Next make a filesystem (mkfs; page 439) on each partition that is to hold a filesystem (not swap). Make all partitions, except swap and /boot, of type ext3, unless you have a reason to do otherwise. Make the /boot partition of type ext2. Use mkswap (page 479) to set up a swap area on a partition. You can use e2label (page 439) to label partitions.

## KEEPING USERS INFORMED

One of your primary responsibilities as a system administrator is communicating with system users. You need to make announcements, such as when the system will be down for maintenance, when a class on some new software will be held, and how users can access the new system printer. You can even start to fill the role of a small local newspaper, letting users know about new employees, RIFs, births, the company picnic, and so on.

Different communications have different priorities. For example, information about the company picnic in two months is not as time sensitive as the fact that you are bringing the system down in 5 minutes. To meet these differing needs, Linux provides different ways of communicating. The most common methods are described and contrasted in the following list. All of these methods are generally available to everyone, except for the message of the day, which is typically reserved for Superuser.

- **write**
  Use the write utility (page 172) to communicate with a user who is logged in on the local system. You might use it, for example, to ask a user to stop running a program that is bogging down the system; the user might reply that he will be done in 3 minutes. Users can also use write to ask the system administrator to mount a tape or restore a file. GNOME opens a new window when it receives a message.

- **wall**
  The wall (write all) utility effectively communicates immediately with all users who are logged in. It works similarly to write, except that users cannot use wall to write back to only you. Use wall when you are about to bring the system down or are in another crisis situation. Users who are not logged in will not get the message.

  Use wall while you are Superuser only in a crisis situation; it interrupts anything anyone is doing.

- **Email**
  Email is useful for communicating less urgent information to one or more systems and/or remote users. When you send mail, you have to be willing to wait for each user to read it. The email utilities are useful for reminding users that they are forgetting to log out, their bills are past due, or they are using too much disk space.

  Users can easily make permanent records of messages they receive via email, as opposed to messages received via write, so they can keep track of important details. It would be appropriate to use email to inform users about a new, complex procedure, so each user could keep a copy of the information for reference.

- **Message of the day**
  Users see the message of the day each time they log in a textual environment. You can edit the /etc/motd file to change this message as necessary. The message of the day can alert users to upcoming periodic maintenance, new system features, or a change in procedures.

## CREATING PROBLEMS

Even experienced system administrators make mistakes; new system administrators just make more mistakes. Although you can improve your odds of avoiding problems by carefully reading and following the documentation provided with software, many things can still go wrong. A comprehensive list is not possible, no matter how long, as new and exciting ways to create problems are discovered every day. A few of the more common techniques are described here.

### Failing to Perform Regular Backups

Few feelings are more painful to a system administrator than realizing that important information is lost forever. If your system supports multiple users, having a recent backup may be your only protection from a public lynching. If it is a single-user system, having a recent backup certainly keeps you happier when you lose a hard disk.

### Not Reading and Following Instructions

Software developers provide documentation for a reason. Even when you have installed a software package before, carefully read the instructions again. They may have changed, or you may simply remember them incorrectly. Software changes more quickly than books are revised, so no book should be taken as offering foolproof advice. Instead, look for the latest documentation online.

### Failing to Ask for Help When Instructions Are Not Clear

If something does not seem to make sense, try to find out what does make sense—do not guess. Refer to “Help” on page 1033.

### Deleting or Mistyping a Critical File

One sure way to give yourself nightmares is to execute the command

```
# rm -rf /etc
# do not do this
```

Perhaps no other command renders a Linux system useless so quickly. The only recourse is to reboot into rescue mode (page 411) and restore the missing files from a recent backup. Although this example depicts an extreme case, many files are critical to proper operation of a system. Deleting one of these files or mistyping information in one of them is almost certain to cause problems. If you directly edit `/etc/passwd`, for example, entering the wrong information in a field can make it impossible for one or more users to log in. Do not use `rm -rf` with an argument that includes wildcard characters; do pause after typing the command, and read it before you press `return`. Check everything you do carefully, and make a copy of a critical file before you edit it.

> **Be careful when using a wildcard character with `rm`**
>
> When you must use a wildcard character, such as *, in an argument to an `rm` command, first use `echo` with the same argument to see exactly which files you will be deleting. This check is especially important when you are working as `root`.
