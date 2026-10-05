
The following sequence of commands defines a 300-megabyte, bootable, Linux
partition 1 on a clear disk:

```
$ sudo /sbin/parted /dev/sdb
```

```
using /dev/sdb                               (create new partition)
(parted) mkpart                             (select primary partition)
Partition type? primary/extended? primary  (default to an ext2 filesystem)
File system type? [ext2]?                           (start at the beginning of the disk)
Start? 1                                     (specify a 300-megabyte partition)
End? 300m                                    (use help to check the syntax of the set command)
(parted) help set
SET NUMBER FLAG      change a flag on partition NUMBER
```

NUMBER is the partition number used by Linux. On mdos disk labels, the primary
partitions from 1 to 4, logical partitions from 5 onwards.
FLAG is one of: boot, root, swap, hidden, raid, lvm, lba, hp-server, palo,
prep, msftres
STATE is on: off,

```
(parted) set 1 boot on             (turn on the boot flag on partition 1)
(parted) print                      (verify that the partition is correct)
```

Disk geometry for /dev/sdb: 0kB - 250GB
Disk label type: mdos

| Number | Start | End | Type | Size | File system | Flags |
|---|---|---|---|---|---|---|
| 1 | 1kB | 300MB | 300MB | primary | ext2 | boot |
(parted)|

Information: Don't forget to update /etc/fstab, if necessary.

When you specify a size within parted, you can use a suffix of k (kilobytes), m
(megabytes), or g (gigabytes). After creating a partition, give a print command to
see where the partition ends. Perform this task before defining the next contiguous
partition so you do not waste space. After setting up all the partitions, exit from
with a quit command.

Next make page 458 on each partition that is to hold a file-system (not swap). Make all partitions, except swap and /boot, use ext4, unless you have a reason to do otherwise. Make the /boot partition of type ext2. Use mkswap (page 498) to set up a swap area on a partition. You can use e2label (page 458) to label a partition.

# KEEPING US INFORMED

One of your primary responsibilities as a system administrator is communicating
with users. You need to make announcements, such as when the system will be for maintenance, when a class on new software will be held, and
how users can access the new system printer. You can even start to fill the role of
small local newspaper, letting users know about new employees, RIFs, births, the
company picnic and so on.

# CREATING PROBLEMS

Different communications have different priorities. For example, information about the company picnic in two months is not time sensitive as the fact that you are bringing the system down in five minutes. To meet these needs, Linux provides different ways of communicating. The most common methods are described and contrasted in the following list. All of these methods are generally available to everyone, except for the message of the day, which is typically reserved for a user with root privileges.

Use the utility (page 124) to communicate with a user who is logged in the local system. You might use it, for example, to ask a user to stop running a program that is slowing the system; the user might reply that he be done in three minutes. Users can also use write to ask the system administrator to mount a tape or restore a file. Messages sent from wall may not appear in a graphical environment.

The wall (write all) utility effectively communicates immediately with all users who are logged in. This utility takes its input from standard input and works like write, except that users cannot use wall to write back to you. Use wall when you are about to bring the system down or in another crisis situation. Users who are not logged in will not get the message.

Run wall as a user with root privileges only in a crisis situation; it interrupts anything anyone is doing. Messages sent from wall may not appear in a graphical environment.

Email is useful for communicating urgent information to one or more systems and/or remote users. When you send mail, you have to be waiting for them to read it. Email is useful for reminding users that they are forgetting to log out, their bills are past due, or they are using too much disk space.

Users can easily make permanent records of messages they receive via email, as opposed to messages received via write, so they can keep track of important details. For instance, it would be appropriate to use email to inform users about a new, complex procedure, so each user could keep a copy of the information for reference.

Users see the message of the day each time they log in a textual environment, but not when they open a terminal window. You can edit the /etc/motd file to change this message as necessary. The message of the day can alert users to upcoming maintenance, new system features, or a change in procedures.

# CREATING PROBLEMS

Even experienced system administrators make mistakes; system administrators make just more mistakes. Although you can improve your odds of avoiding problems by carefully reading and following the documentation provided with software, many things can still go wrong. A comprehensive list, no matter how long, is not possible because new and exciting ways to create problems are discovered every day. This section describes a few of the more common techniques.

# 616 CHAPTER 16 ADMINISTRATION TASKS

Failing to perform regular backups Few feelings are more painful to a system administrator than realizing that information is lost forever. If the local system supports multiple users, having a recent backup may be your only protection. If it is a single-user system, having a recent backup keeps you happy when you lose disk.

Not reading and following instructions Software developers provide documentation for a reason. Even when you have installed software package, carefully read the instructions. They may have changed, or you may simply remember them incorrectly. Software changes more quickly than books are revised, so no book should be taken as proof. Instead, look for the latest documentation online. The /usr/share/doc directory has information on many utilities, libraries, and software packages.

Failing to ask for help when instructions are not clear If something does not sense, try to find out what makes sense—do not guess. See Appendix B for a list of places you may be able to find assistance.

Deleting or mistyping information in a critical file One way to give nightmares useless is to execute the command

```
$ rm -rf /etc <-- do not do
```

Perhaps no other command renders a Linux system useless so quickly. The only recourse is to reboot into recovery mode using CD/DVD (page 445) and restore the files from a recent backup. Although this depicts an extreme case, many files are critical to proper operation of a system. Deleting one of files or mistyping information in one of them is almost certain to cause problems. If you directly edit /etc/passwd, for example, entering the wrong information in a field can make it impossible for one or more users to log in. Do not use -rf with an argument that includes wildcard;; after typing the command, and read it before you press RETURN. Check everything you do fully, and make a copy of a critical file before you edit it.

> Be careful when using a wildcard character with rm

When you must use a wildcard character, such as *, in an argument to an rm command, first use echo with the same argument to see exactly which files you be deleting. This check is especially when you are working with root privileges.

# SOLVING PROBLEMS

As the system administrator, it is your responsibility to keep the system secure and running smoothly. When a user has a problem, it usually falls to the administrator to help the user get back on track. This section suggests ways to keep users happy and the system functioning at peak performance.

# HELPING WHEN A USER CANNOT LOG IN

When a user has trouble logging in on the system, the source may be a user error or a problem with the system software or hardware. The following steps can help determine where problem is:
