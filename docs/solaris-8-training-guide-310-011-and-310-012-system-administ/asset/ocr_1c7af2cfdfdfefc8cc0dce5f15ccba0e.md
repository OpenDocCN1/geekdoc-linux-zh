# Device Auto-Configuration

Auto-configuration offers many advantages over the manual configuration method used in earlier versions of UNIX, in which device drivers were manually added to the kernel, the kernel was recompiled, and the system had to be restarted. Now, with auto-configuration, the administrator simply connects the new device to the system and performs a reconfiguration startup.

# STEP BY STEP

# 16.1 Performing a Reconfiguration Startup

+   1. Create the /reconfigure file with the following command:
   `touch /reconfigure`

   The /reconfigure file causes the Solaris software to check for the presence of any newly installed devices the next time you turn on or start up your system.

2. Shut down the system using the shutdown procedure described in Chapter 1, “System Startup and Shutdown.”

   If you need to connect the device, turn off power to the system and all peripherals after Solaris has been properly shut down.

   After the new device is connected, restore power to the peripherals first and then to the system. Verify that the peripheral device has been added by attempting to access it.

> NOTE
The file named /reconfigure automatically gets removed during the boot-up process.

An optional method of performing a reconfiguration startup is to interrupt the start process and type boot -r at the OpenBoot prompt.

I prefer the first method described because the system administrator can instruct the system to perform the reconfiguration startup at any time by creating the /reconfigure file. Now, at the next restart, whether the administrator is there or not, the system performs the reconfiguration startup. This could happen at 3 a.m. if you like.

> NOTE
As root, you can also issue the reboot -- -r command from the UNIX shell. The -- -r passes the -r to the boot command.