The last popular kernel with the "memory problem", 2.0.36, comes with RedHat 5.2. My RedHat 6.0 came with kernel 2.2.5-15 so it does not have the "memory problem" any more.

To get more than 64 MB memory recognized on RH5.2, you have to edit (as root) file /etc/lilo.conf, and add a line like this just before your first "image=" statement:

```
append=mem=80M
```

If you have an amount of memory different than 80 MB, adjust the above line. For any changes in /etc/lilo.conf to take effect, you*must re-run the program

# lilo

(watch if it runs without errors) and reboot. At the reboot, you can check if your adjustment working using either of these commands:

```
cat /proc/meminfo
```

```
free
```

For testing purposes, or if you are having problems, the option of specifying the amount of memory at the LILO prompt is:

[type at LILO prompt during boot] linux "mem=16M"

Occasionally, I hear the device to skip the few megabytes if you have problems enabling your memory, or the machine locks up. E.g., enable only 78 out of your 80 MB. This is apparently the case for some SCSI controllers that use the upper chunk of the main memory. Take it for what it's worth.

Occasionally on some systems, Linux recognizes only 16 MB of memory. This is usually linked to the setting "memory hole at 15-16 MB" in the BIOS setup (the solution is to disable this BIOS setting). It is probably good to disable "advanced" features in your BIOS setup anyway (for example, the BIOS virus detection can be a common source of problems ).

Mi of memory chips with different timings can lead to memory problems or system crashes (the solution is to replace the memory chips so that the timing of all memory chips is the same).

# 4.1.2 LILO displays only LI (or LIL) and hangs

I quote from my good handbook "Red Hat Linux Unleashed" by Kamran Hussain, Timothy Parker, et al., published by SAMS Publishing:

"When LILO loads itself, it displays the word LILO. Each letter is printed before or after performing some specific action. If LILO fails at some point, the letters printed so far can be used to identify the problem. [...]"