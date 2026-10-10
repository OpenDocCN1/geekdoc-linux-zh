If Corel Linux will share space with an existing Windows system, it helps to defragment your hard drive before you begin. In Windows, choose Start➜ Programs➜ Accessories➜ System Tools➜ Disk Defragmenter.

Table 2-2 **Where to Install**

| "Where" Option | Pros | Cons |
| :----- | :----- | :----- |
| Take over disk | Simple, clean way to set up a Linux-only machine<br>Zero sweat if you’re starting from a virgin machine | Wipes out existing systems and data<br>Leaves no room for another operating system |
| Use free disk space | Preserves existing systems and data<br>Let’s Linux coexist with another OS | Must have unpartitioned space not used by another OS; see the “When free space isn’t free” section<br>Existing disk structure may not allow this, even where there is space |
| Edit partition table | Let’s you allocate separate partitions for specific files (user directories, additional programs, temporary files, and so on), especially on a multiuser system or network server<br>Let’s you escape limitations of your system BIOS, especially when the kernel resides below cylinder 1023<br>Allows you to reinstall Corel Linux or remove another version of Linux before installing | Can destroy existing systems and data with one mouse click<br>Extra partitions can waste space<br>You can’t resize existing partitions to free up space with Install Express |
| Install in DOS/ Windows partition | Let’s you try Corel Linux in Windows 95/98 without reformatting all or part of your disk | Inefficient way to run Corel Linux<br><br><br>Awkward to reboot between Linux and Windows |