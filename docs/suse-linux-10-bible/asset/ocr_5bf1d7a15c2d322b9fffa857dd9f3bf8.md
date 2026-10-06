In both cases, the 1 tells to load up the system in runlevel 1. This, as you may remember, the runlevel that signifies single-user mode with no network. This is the lowest usable runlevel that is needed only if there is a problem with the system.

![](bbox=[0.181, 0.21, 0.809, 0.589])

**Figure 4-3:** Adding the runlevel to the GRUB boot loader

On

As shown in Figure 4-4, you will be asked for the password to log in the system (this is why you should *never* forget your root password). Once logged in you can then off processes as we talked about with the `chkconfig` script or fix any other problems that the system has. Once fixed, you can then reboot the system normally. Because specifying a runlevel to GRUB and LILO is a temporary change, you are able to let the system start up normally without having to interrupt the normal operation of LILO or GRUB.