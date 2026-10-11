![](bbox=[0.06, 0.12, 0.83, 0.45])

Many of these devices are part of a default installation, others you add to the system over time as you add components using commands like the *drvconfig* command. When you do a reconfiguration reboot, *drvconfig* is automatically run and reads the file permission information for new devices from the /etc/minor_perm file, which points the *drvconfig* utility to new nodes in the device tree and then adds a file to the /dev directory.
The *drvconfig* command creates device drivers for physical devices and logical or pseudo drivers for logical devices. Devices form a /devices directory tree that is read and executed at startup by your system. Often, the best way to solve a recalcitrant device problem (particularly one that is software related) is to reboot your system and reinitialize the software.

# Device Types

To see the contents of the /dev directory, use the 1s -lL command. The -L option displays the contents of the /dev directory by names rather than as symbolic links to the /devices directory. In a typical entry returned from the command, you would see the following:
`crw-rw-rw- 1 root sys 13 12 Mar 12 08:05 zero`
Here, the initial character tells you what the link type is: *b* for block, *c* for character, *d* for directory, *D* for door, *l* for symbolic link (or named pipe), and *s* for AF-UNIX sockets.