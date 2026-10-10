# **Table 3-1 Virtual Partitions States**

| vPars State | Description |
|---|---|
| load | The kernel image of a Virtual Partition is being loaded into memory. This is done by the Virtual Partition monitor. |
| boot | The Virtual Partition is in the process of booting. The kernel image has been successfully loaded by the Virtual Partition monitor. |
| up | The Virtual Partition has been successfully booted and is running. |
| shut | The Virtual Partition is in the process of shutting down. |
| down | The Virtual Partition is not running and is down. |
| crash | The Virtual Partition has experienced a panic and is crashing. |
| hung | The Virtual Partition is not responding and is hung. |

We have seen several of these states in Chapter 2 when we created Virtual Partitions and watched them boot by issuing successive **vparstatus** commands. The following example shows the process of the Virtual Partition *cable2* booting:

```
```text
# vparboot -p cable2
# vparstatus
[Virtual Partition]
Virtual Partition Name  State Attributes Kernel Path Boot Opts
------------------------------------------
cable1 Up Dyn.Manl /stand/vmunix
cable2 Load Dyn.Manl /stand/vmunix

[Virtual Partition Resource Summary]
Virtual Partition Name CPU Num Memory (MB)
                        Min/Max Bound/ IC # Ranges/ Total MB
                        Unbound devs /stand/vmunix
cable1 2/4 2 0 4 0/0 2048
cable2 2/2 2 0 4 0/0 1024
# vparstatus
[Virtual Partition]
Virtual Partition Name State Attributes Kernel Path Boot Opts
------------------------------------------
cable1 Up Dyn.Manl /stand/vmunix
cable2 Boot Dyn.Manl /stand/vmunix

[Virtual Partition Resource Summary]
Virtual Partition Name CPU Num Memory (MB)
                        Min/Max Bound/ IC # Ranges/ Total MB
                        Unbound devs /stand/vmunix
cable1 2/4 2 0 4 0/0 2048
cable2 2/2 2 0 4 0/0 1024
# vparstatus
[Virtual Partition]
Virtual Partition Name State Attributes Kernel Path Boot Opts
------------------------------------------
cable1 Up Dyn.Manl /stand/vmunix```
```