will crash! The first sign that you are running out of paging space consists of a bunch of weird errors, for example:

```
```
Fork failure - not enough memory available
Fork function not allowed. Not enough memory available
fork() system call failed
Unable to fork, too many processes
ksh: cannot fork not enough swap space
INIT: Paging space is low
Not enough memory
```
```

# ## Adding a Paging Space

Paging space requirements depend on the amount of real memory in your system. During the BOS installation process, paging space is created automatically; however, it is never enough to do any heavy work. If real memory is greater than or equal to 64MB (the minimum for AIX5L) the system will create a single paging space equal to real memory plus 16MB. This is not enough paging space! The actual amount of paging space required depends on the applications you are running and how much real memory is in the system. Any database (DB2, Oracle, or Sybase) needs a lot of memory and paging space. On our SAP systems, the requirement for memory is 4GB as a minimum and the paging space requirement is in the tens of gigabytes! You need to do some research on your application requirements before setting up your paging space.

There are two commands that will display the amount of real memory in your system. Both commands report resident memory in kilobytes:

```
```
lsattr -El sys0 | grep realmem
bootinfo -r
```
```

You need to monitor how your system is using paging space to know if you have enough. You can monitor each paging space with the **lspfs -a** command, and you can get a summary of all paging spaces put together using the **lspfs -s** command. The default system paging logical volume is hd6. Each additional paging space logical volume will be assigned paging00, paging01, and so on.

Here is a listing of paging space best practices:

+   1. Each paging space should be pretty close to the same size. The VMM uses a round-robin technique to attempt to balance paging space usage.
+   2. It is not advisable to put more than one paging space on a single disk! Placing each paging space on a separate disk helps to minimize any disk I/O bottleneck and ensures that the round-robin technique used for paging space size is not defeated. However, your paging space should be mirrored just as you should mirror the root volume group.
+   3. Never extend a paging space to span multiple disks. Since the VMM is using a round-robin technique, the disk activity will be unbalanced.