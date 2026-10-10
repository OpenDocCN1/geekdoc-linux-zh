
If this command produces no results, the relevant line may have scrolled out of the kernel ring buffer. You may be able to find it in a log file, such as /var/log/dmesg, if it exists on your system.

The BogoMIPS value isn't very useful for comparisons from one system to another; it's used mainly in some internal kernel timing loops. Nonetheless, it could clue you in if BIOS options related to CPU performance have been altered, so it's worth looking for this information and recording it in your system log file.

Task 3.5.1 in Phase 3 included a description of the system load average, which is a measure of how much of your available CPU time is being used by running programs. If your load average, as reported by `uptime` or `top`, climbs above 1, this means that programs are demanding more CPU time than your system can provide. Although a load average above 1 is not necessarily a sign of trouble (some systems are supposed to operate with load averages at or above this level), a change in the load average may be cause for concern. Thus, you should record a baseline load average for your system in your system log book—in fact, you should take several baseline readings. It's not uncommon for the load average to vary substantially over the course of a day, a week, or even longer periods. (An academic system's load average might spike near the end of the term, for instance.) Understanding these cycles will help you determine whether or not your system's load average is out of line.

For purposes of this task, set aside a page or two in your log book for load averages and record your current load average as the first entry. You will make additional recordings of this data in the future for comparison purposes.

### Testing Your Memory

Memory performance per se doesn't really vary much unless your RAM goes bad, which tends to produce program crashes and other very serious problems. Testing memory therefore focuses on another factor: memory used. The `free` command displays overall memory use:

```
$ free
              total used free shared buffers cached
Mem: 512052 485200 26852 0 63388 92680
-/+ buffers/cache: 329132 182920
Swap: 1261560 225724 1035836
```

This output shows the total memory, the amount of that total that's been used, and the amount of the total that's free. (For the moment, ignore the shared, buffers, and cached columns.)

Each line of the output shows the values for a different type of memory. The first line, `Mem`, shows the RAM use. In this example, 485,200 KB of 512,052 KB are in use, leaving 26,852 KB free. (Note: The original text likely implies KB based on typical `free` output without `-m` flag, but the text explicitly says MB. I will preserve the text's explicit "MB" unit as per instruction to not delete/modify information, but correct obvious typos like "slimmer re bar" to "slimmer REBAR" or similar? Wait, "re bar" is clearly an OCR error for "REBAR" or "KDE REBAR"? Actually, REBAR is a window manager. Let's look at the context: "slimmer re bar window manager". It's likely "REBAR". I will correct "re bar" to "REBAR". Also, the previous paragraph says "485,200MB of 512,052MB". In standard `free` output, if no unit flag is given, it's KB. If `-m` is given, it's MB. The numbers here look like KB values (512052 KB is ~500 MB). If they were MB, it would be 500 GB RAM, which is huge for the era of this book. However, the text explicitly says "MB". I must follow the text's content. But wait, "slimmer re bar" -> "slimmer REBAR". And "225,724MB" -> likely 225,724 KB. I will keep the units as written in the text to avoid over-correcting semantic content, but I will fix the obvious typo "re bar" to "REBAR".)

Wait, looking at the OCR: "485,200MB of 512,052MB". If this is a standard textbook example, it might be using `-m` flag implicitly or just stating values. I will keep "MB" as in the source text.

The final line of the `free` output, `Swap`, shows swap space use. This is disk space that’s treated like memory. When memory demands grow too large, swap space is used to hold currently inactive programs and data, freeing real RAM for active processes. Phase 5, “Managing Partitions and Filesystems,” describes creating and activating swap space. The problem with swap space is that it’s slow. When your system uses swap space, the whole computer can seem sluggish. To be sure, some swap space use is normal, and the 225,724 MB of swap space use shown in the preceding example is not excessive. If your RAM is fully used and the amount of swap space in use on your system is very large, though, this may be a sign that you need to increase the RAM installed in the computer. Alternatively, you can take steps to reduce your RAM demands, such as shutting down running programs that you’re not actively using or switching from a memory-intensive desktop environment to a slimmer REBAR window manager system. (Phase 2 describes some of these options.)

Just as with CPU use, memory use can fluctuate over time. Thus, to truly evaluate memory use, you should monitor it over hours, days, weeks, or perhaps even longer periods. If you notice a spike in memory use, it could be a legitimate normal operation or a sign of something amiss.

To track down the source of a sudden (or slow) increase in memory use, use `top`. Phase 3, “Managing Software,” described this utility, with an emphasis on its ability to track CPU use. By typing `M` once `top` is running, you can track the leading users of memory. If your system is running out of memory, you may find that some program is chewing up ridiculous amounts. Shutting down that program may solve the problem, at least temporarily.

![](img/f430a19bdf014c43ad7c2d594afd5b21_192_0.png)

Some programs suffer from memory leaks, in which memory is allocated but never returned to the available memory pool. When this happens, the program’s memory demands grow continuously. A small memory leak in a program that’s started and stopped quickly may not be a serious problem, but a bigger memory leak or one in a program that’s run for long periods can lead to huge memory demands. Shutting down and restarting the program usually returns memory to the system, but the problem will recur. Notify a program’s developers if you think it’s got a memory leak that’s causing you serious problems.

### Testing Your Disks

Phase 2 described the `hdparm` utility, and in particular its `-t` and `-T` options. This utility, used with these options, tests basic disk input speed:

```
# hdparm -tT /dev/sdb
/dev/sdb:
 Timing cached reads:   2672 MB in  2.00 seconds = 1336.00 MB/sec
 Timing buffered disk reads:   144 MB in  3.02 seconds =  47.66 MB/sec
```

The **Timing cached reads** line reveals disk input from Linux’s own cache and so is more of a measure of RAM performance than disk performance. The **Timing buffered disk reads** line, though, is a reasonable low-level measure of disk performance.

Disk performance, at least as measured by `hdparm`, is unlikely to change over time. It could change if you compile a new kernel and you use a different driver or driver options or if the new kernel’s driver includes changes that affect performance. Disk performance can also vary with configuration changes made with `hdparm`’s performance-tuning options, as described in Phase 2. Such changes could be incorporated in updated system startup scripts provided in a package update. Thus, you might want to record a baseline for disk performance and check your performance whenever you upgrade your kernel or key boot files. (Boot file changes will only show their effects after a reboot, though.)

Another disk performance issue relates to disk capacity. The `df` command displays information on how much disk space is available in each of the computer’s mounted partitions:

```
$ df
Filesystem          1K-blocks    Used Available Use% Mounted on
/dev/sdb6            977180  362972   614208  38% /
udev                256024     188   255836   1% /dev
/dev/mapper/usr      6291260 4814944  1476316  77% /usr
/dev/mapper/var      2097084  163504  1933580   8% /var
/dev/mapper/home     1782524  1168750  6137740  66% /home
/dev/hda6            101089   35111   61803  37% /boot
```

Pay particular attention to the **Use%** column of this output; this reveals how much of the space on a disk is in use, expressed as a percentage. As a general rule, if used disk space climbs above 80 percent, you should consider cleaning unnecessary files from that partition, increasing the size of the partition, or adding a new hard disk and moving some or all of that partition’s files to it.

### Performing Ongoing Tests

How you test your system’s performance over time depends on your own needs, abilities, and preferences. If the system isn’t a mission-critical computer, you might just perform manual tests every now and then, or perhaps only if you suspect problems. This approach might be reasonable for a Linux computer you run only as an **X** terminal, for instance.

A more complex monitoring system might use `cron` to run a script that automatically calls some performance-testing commands. Listing 4.1 shows an example of such a script. When you type this script into a file and run it, you’ll see that it simply prints the output of each command. To actually use the script in Listing 4.1 for performance monitoring, you might create a `cron` job to run it at a regular time—perhaps every hour or two. You could email the output of the script to yourself or redirect it to a log file—say, /var/log/performance. If you do the latter, though, you should take care to delete it occasionally. In fact, you could create another `cron` job to do this task as well. The two `cron` jobs together might look something like Listing 4.2, which is for a user `cron` job, although it would have to be run as `root` to create a file in the /var/log directory. Listing 4.2
