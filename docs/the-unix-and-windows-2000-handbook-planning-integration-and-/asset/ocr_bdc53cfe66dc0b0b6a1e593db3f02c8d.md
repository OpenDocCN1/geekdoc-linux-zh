The # symbol denotes a comment and everything to the right of it is ignored. In this case, we are calling the Matlab license manager, /etc/lmboot. The logic call if ends with the close call fi. The test [-f /etc/lmboot ] is important. It checks to see if the file exists, then executes it and displays a line confirming that you have executed the script. When adding your own additions, always use the -f predicate to confirm that the file is there before executing; printing the confirmation makes it much easier to debug if the startup script is hanging.

> As mentioned before, these scripts are just Bourne shell scripts, so any of the logic available to a Bourne script is available in the rc scripts. A major rule of thumb is to keep it simple. Another rule is never to remove code from an rc script. If you wish to disable lines, use the # symbol to make them comments. A great deal of the code found in an rc script is system-dependent, and re-creating it would be very difficult. Do not edit these scripts unless it is absolutely necessary.

# Following the System V Startup Scripts

The System V (SysV) startup process is more complicated, and likewise offers more options. Instead of the three run levels found in BSD, the SysV startup has eight. The run levels are 0-6 and s (or S) for single-user. Each run level has a different functionality. The run levels are defined by a series of scripts that are called by init. The relationship between run levels and scripts is contained in the system file, inittab. The run levels are shown in Table 3.2.

# INITTAB

The run levels above are controlled by a file named /etc/inittab. This file controls the operation of the init process. Following is a sample inittab file from a Solaris 2.6 system:

```
mars# cat /etc/inittab

ap::sysinit:/sbin/autopush -f /etc/iu.ap

ap::sysinit:/sbin/soconfig -f /etc/sock2path

fs::sysinit:/sbin/rcS          >/dev/console 2></dev/console </dev/console

is:3:initdefault:
```