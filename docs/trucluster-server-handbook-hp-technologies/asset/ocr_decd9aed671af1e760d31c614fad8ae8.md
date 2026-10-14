# # volencap swap

Setting up encapsulation for dsk2b.
- Creating simple disk dsk2f for config area (privlen=4096).
- Warning: space taken from -> dsk2b dsk2f
- Creating nopriv disk dsk2b for molari-swap.

The following disks are queued up for encapsulation or use by LSM:
dsk2f dsk2b

Please consult the Cluster Administration Guide for steps that you will need to follow to complete the encapsulation.

```
# volreconfig

EXEC: voletit -rf rm molari-swap01
EXEC: voldg rmdisk dsk2b
EXEC: voldisk rm dsk2b
lsm:voldisk: ERROR: Failed to obtain locks:
dsk2b: no such object in the configuration
The system will need to be rebooted in order to continue with
LSM volume encapsulation of:
dsk2f dsk2b
```

At this point the volreconfig command will prompt you to reboot the system. We will give the users five minutes.

```
Would you like to either quit and defer encapsulation until later or commence system shutdown now? Enter either 'quit' or time to be used with the shutdown(8) command (e.g., quit, now, 1, 5): [quit] 5

Shutdown at 13:45 (in 5 minutes) [pid 525876]
#
*** System shutdown message from root@molari.tcrhb.com ***
System going down in 5 minutes
... Place selected disk partitions under LSM control.
..
System going down in 2 minutes
..
System going down in 60 seconds
-
System going down in 30 seconds
```

You can encapsulate all cluster members' swap partitions by specifying all the devices as parameters to the volencap command and then issuing the volreconfig command on every member, but