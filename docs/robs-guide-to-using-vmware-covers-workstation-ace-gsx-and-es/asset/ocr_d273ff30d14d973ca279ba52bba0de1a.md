![](bbox=[0.05, 0.07, 0.93, 0.5])

Figure 6.5: Always return to the same starting point with snapshots.

3. Close the VMware application and enter the gui.restricted = "true" parameter in the .vmx file.

From now on, the virtual machine will always start with the same state of operating system that it was in when the snapshot was created.

# 6.8 VMware Guest Time Synchronization

Time synchronization between the host computer and the guest is a mechanism which either: always works for you, or always gives you a headache. Let's get it over with, and look at the details of configuring time synchronization.

A new virtual machine boots and takes over the time from the host operating system. It creates a NVRAM BIOS file which is also used to store the values of the CMOS clock of the virtual machine. Just as with a real PC, the virtual machine uses its internal clock, and your guest operating system in turn uses that time.