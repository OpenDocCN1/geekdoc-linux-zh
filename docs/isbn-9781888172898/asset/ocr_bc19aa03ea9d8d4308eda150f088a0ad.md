+   - run [-t fs] dev:file - Boot Linux from the specified device and file
+   - run [-t fs] dev:file - Run the standalone program dev:file
+   - show - Display all known devices and file systems
+   - set VAR VALUE - Set the variable VAR to the specified VALUE
+   - unset VAR - Delete the specified variable
+   - reset - Delete all variables
+   - print - Display current variable settings
+   - help [var] - Print this help text

Devices are specified as: fd0, hda1, hda2, sda1... Use the '-t filesy stem-name' option if you want to use anything but the default filesystem ('ext2'). Use the 'show' command to show known devices and file systems. Type 'help var' for a list of variables.

Note that the bootopt command only appears on AlphaPC64 (and similar) systems. Refer to the board's documentation to find out just what it means.

Devices. Until you use a command that needs to make use of a device, no device initialisation will take place. The first show, ls, boot or run commands all cause the devices within MILO to be initialised. Devices are named in the same way (exactly) that Linux itself will name them. So, the first IDE disk will be called 'hda' and its first partition will be 'hda1'. Use the show command to show what devices are available.

File Systems. MILO supports three file systems, MSDOS, EXT2 and ISO9660. So long as a device is available to it, MILO can list,boot or run an image stored on one of these file systems. MILO's default file system is EXT2 and so you have tell MILO that the file system is something other than that. All of the commands that use filenames allow you to pass the file system using the -t [filesystem]option. So, if you wanted to list the contents of a SCS1 CD ROM, you might type the following:

```
MILO> ls -t iso9660 scd0
```

Variables. MILO contains some settable variables that help the boot process. If you are loading via the Windows NT ARC firmware, then MILO makes use of the boot option environment variables set up by that firmware. For some systems, MILO (for example, the AlphaPC64) maintains its own set of environment variables that do not change from boot to boot. These variables are: