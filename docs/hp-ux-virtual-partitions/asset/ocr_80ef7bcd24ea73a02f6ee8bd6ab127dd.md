time it takes at boot to write the core dump in primary swap to a file, you may want to forgo adding a specific dump device to your system.
Since you probably won't be allocating an entire disk as a dump device, you may be using a logical volume. You must select a logical volume in the root volume group that is unosed or is used for non-file-system swap. This is done by selecting *Add* from the *Actions* menu to add a disk or logical volume to the list of dump devices.

You will want to get acquainted with the *View Dump Configuration Details* subarea of *Dump Devices*. It is here where you can see what the current dump configuration is, what the current and pending kernel dump configurations are, and what the current runtime dump configuration is.

# Subsystems

Selecting *Subsystems* lists all of your subsystems. For each subsystem, the following information is listed:

+   * *Name* - Name of the subsystem.
+   * *Current Value* - Lists whether the subsystem is *In* or *Out of /stand/vmunix*.
+   * *Pending Value* - Lists whether the subsystem is *In* or *Out* of the pending kernel.
+   * *Description* - A few words describing the parameter.

You can then take a number of *Actions*, including the following:

*Templates* You can select a kernel template to load that is basically a different kernel configuration from the one you are currently running.

*Process New Kernel* After making whatever changes you like to the *Pending State* of a subsystem, you can have SAM create a new kernel for you.

*View Subsystem Details*