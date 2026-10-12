When you see the LILO boot: prompt, type the name you assigned to the new kernel in the /etc/lilo.conf file. You do not have to type anything if you added the new kernel description as the first entry in the LILO configuration file.

After the system reboots, you should see the familiar graphical login screen. To see proof that you are indeed running the new kernel, log in as a user, open a terminal window, and type uname -srv. This command shows you the kernel version as well as the date and time when this kernel was built. If you upgraded the kernel source, you should see the version number for the new kernel. If you simply rebuilt the kernel for the same old kernel version, the date and time should match the time when you rebuilt the kernel. That's your proof that the system is running the new kernel.

![](bbox=[0.13, 0.35, 0.23, 0.42])

If the system hangs (nothing seems to happen — there is no output on the screen and no disk activity), you may have skipped a step during the kernel rebuild. You can power the PC off and on to reboot again. This time, enter linux (the old working kernel's name) at the LILO boot: prompt.

If you cannot boot the older version of Red Hat Linux either, use the emergency boot disk (containing an earlier, but working, version of Linux) to start the system. Then you can repeat the kernel rebuild and installation process making sure that you follow all the steps correctly.

![](bbox=[0.01, 0.45, 0.09, 0.54])

# REVIEW

In this session, you learned how to install the kernel source files and configure the kernel using the make xconfig command. Then you learned the command to build a new kernel and new driver modules. You also learned the procedure for installing the new kernel so that you can boot the system and start using the newly built kernel.

# QUIZ YOURSELF

+   1. What does “rebuilding the kernel” mean and what are the key phases of rebuilding the kernel? (See “Installing the Source Files and Rebuilding the Kernel”.)