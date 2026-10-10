| table2 | Up | Dyn_MemI | /stand/vmunix |
|---|---|---|---|
| [Virtual Partition Resource Summary] | CPU<br>Min/Max | CPU<br>Bound | Num IO<br>devs | Memory (MB)<br># Ranges/Total MB | Total MB | |
| table1 | 2/4 | 2 0 | 4 | 0/0 | 2048 | |
| table2 | 2/2 | 2 0 | 4 | 0/0 | 1024 | |

This example shows table2 progressing through the load, then boot, and finally, up. table2 was booted from table1 running on the same hardware. The system had already gone through the boot process when table1 booted. The boot time for table2 is very quick since most of the hardware is already running. The boot time for the first Virtual Partition is comparable to the boot time of a non-Virtual Partition system, but the subsequent vPars boot much more quickly.

# ## setboot Command and vPars

In our example vPars in Chapter 2, we had autoboot set to off for our Virtual Partition. The setboot command on a non-vPars system reads from and writes to stable storage. On a vPars system the setboot command interacts with the Virtual Partition database. Running setboot on a vPars system has the effects shown in Table 3-2:

# ### Table 3-2 setboot and Virtual Partitions

| vPars setboot Option | Description |
|---|---|
| -a | Changes the alternate boot path of the Virtual Partition. To set the alternate boot path: # setboot -a 0/8/0/0.8,0.5,0.0.0 |