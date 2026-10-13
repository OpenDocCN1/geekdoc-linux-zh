7. Look at the running processes one more time. Type ps and press Enter. You'll notice that your original process (bash) and the most recent execution of the ps command are the only commands running.

# Viewing System Memory Usage

One of the great things about Linux is that it can use computer resources to the fullest advantage. Linux uses a reserved portion of your hard drive, called swap space, to increase the amount of RAM memory resources available to run processes. Linux can make use of the swap space just as if it were RAM.

Because Linux runs processes in system memory (or RAM), it is important to keep track of system memory usage. Now, if you're running a powerhouse machine with 256MB of RAM and the same amount of swap space, this might never be a concern. You might have heard that Linux and the X Window System will run adequately with 16MB of RAM and 16MB of swap space and if you've chosen this route for your bare-bones machine, memory usage will certainly be one of your system management priorities.

The free command displays the amount of memory present on the system. This command enables you to quickly examine how physical (or RAM) memory and virtual (or swap) memory are being used. To use the free command, type free and press Enter at the shell prompt. An example of the free command is used in Listing 13.1.

# LISTING 13.1 The Output of the free Command

```
[root@localhost /root]# free
             total       used       free     shared    buffers     cached
Mem:        79252      77720       1532      49972       6292      28520
-/+ buffers/cache:    42908      36344
Swap:       145112         16     145096
```

![](bbox=[0.18, 0.88, 0.25, 0.95])

> The free command lists memory in kilobytes (one megabyte equals 1024 kilobytes). If you would rather see this information in megabytes, type free -m and press Enter.

Listing 13.1 shows a system with 79 megabytes of RAM, of which about 78MB is being used and 1.5 megabytes are free. It also shows a swap space of 145MB and only 16KB of it is being used. This system is running normally.