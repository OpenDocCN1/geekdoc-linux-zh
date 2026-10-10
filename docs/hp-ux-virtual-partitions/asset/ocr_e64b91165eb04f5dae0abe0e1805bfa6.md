An error was encountered attempting to rewind a device.

**error skipping file**
An error was encountered attempting to forward-space a tape device.

**negative skip count**
The skip count, if specified, must be greater than or equal to zero.

**no major number**
The specified manager has no entry in the block or character device switch tables.

**path incompatible with another path**
Multiple incompatible hardware paths have been specified.

**path long**
The hardware path specified contains too many components for the specified manager.

**path short**
The hardware path specified contains too few components for the specified manager.

**table full**
Too many devices have been specified to hpux.

# EXAMPLES

As a preface to the examples which follow, here is a brief overview of HP-UX system boot-up sequences.

# Automatic Boot

Automatic boot processes on various HP-UX systems follow similar general sequences. When power is applied to the HP-UX system processor, or the system Reset button is pressed, processor-dependent code (firmware) is executed to verify hardware and general system integrity (see pdc(8M)). After checking the hardware, pdc gives the user the option to override the automatic sequence by pressing the Esc key. At that point, a message resembling the following usually appears on the console.

```
(c) Copyright. Hewlett-Packard Company. 1994.
All rights reserved.

PDC ROM rev. 130.0
32 MB of memory configured and tested.

Selecting a system to boot.
To stop selection process, press and hold the ESCAPE key...
```

If no keyboard activity is detected, pdc commences the autoboot sequence by loading isl (see isl(8M)), and transferring control to it.
Since an autoboot sequence is occurring, isl finds and executes the autoboot file which, on an HP-UX system, requests that hpux be run with appropriate arguments. Messages similar to the following are displayed by isl on the console:

```
Booting from: scsi 6 HP 2213A
Hard booted.
Fsi Revision A.02.D9 March 27, 1990
Isl booting hpux boot disk:/0;/stand/vmunix
```

hpux, the secondary system loader, then announces the operation it is performing, in this case boot, the devicefile from which the load image comes, and the TEXT size, DATA size, BSS size, and start address