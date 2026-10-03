# APPLY YOUR KNOWLEDGE

8. List the target number and the device type of each SCSI device attached to your system using the OpenBoot commands in step 7.

9. From the OpenBoot prompt, identify your default boot device as follows:

```
printenv boot-device
```

10. Use the show-disks OpenBoot command to get a listing of the disk drives on your system as follows:

```
show-disks
```

Display the full device path for the disk4 devalias as follows:

```
devalias disk4
```

Create a permanent device alias named disk4 that points to SCSI target 4 as follows.

```
nvalias disk4 /iommu/sbus/espdma@f,400000/esp@f,800000/sd@4,0
```

Reset the system, and verify the devalias is still set by typing the following:

```
reset
devalias disk4
```

11. Boot the system, log on as root, and use the eeprom command to list all NVRAM parameters using the eeprom command.

12. Use the eeprom command to list only the setting of the boot-device parameter as follows:

```
eeprom boot-device
```

13. Reset the boot-device to its default parameter from the OpenBoot prompt as follows:

```
set-default boot-device
```

14. From the OpenBoot prompt, remove the alias disk4 as follows:

```
nvunalias disk4
```

15. Reset the system, and verify disk4 is no longer set as follows:

```
reset
printenv
```

16. Set all the OpenBoot parameters back to their default values as follows:

```
set-defaults
```

# Review Questions

1. The hardware-level user interface that you see before the operating system has been started is called:

A. OpenBoot
B. EEPROM
C. Firmware
D. Boot PROM

2. Which of the following is where the system identification information is stored, such as the hostid?

A. Firmware
B. OpenBoot
C. NVRAM
D. Kernel

3. What task(s) is/are performed by OpenBoot? (Select two.)

A. Executing POST
B. Loading the bootblk
C. Executing ufsboot
D. Loading the OS kernel