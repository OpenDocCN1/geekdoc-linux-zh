constantly trying to free memory. The paging daemon normally runs once a minute or so, but a high $sr$ count means you're probably trying to do more work than your RAM can hold.

# ## Disks

The disks section shows each of your disks by device name. The number shown is the number of disk operations per second, a valuable clue to determining how well your disks are handling their load. You should divide your disk operations between different disks whenever possible and arrange them on different buses when you can. If one disk is obviously busier than the others, and the system has operations waiting for disk access, consider moving some frequently accessed files from one disk to another. One common cause of high disk load is a coredumping program that can restart itself. For example, a faulty CGI script that dumps core every time someone clicks on a link will greatly increase your disk load.

If you have a lot of disks, you might notice that they don't all appear on the vmstat display. Designed for an 80-column display, vmstat(8) can't list every disk on a large system. If, however, you have a wider display and don't mind exceeding the 80-column limit, use the `-n` flag to set the number of drives you want to display.

# ## Faults

Faults aren't inherently bad; they're just received system traps and interrupts. An abnormally large number of faults is bad, of course—but before you tackle this problem, you need to know what's normal for your system.

The first line of vmstat output shows the average faults per second since system boot.

+   - in The number of system interrupts (IRQ requests) received
+   - sy The number of system calls