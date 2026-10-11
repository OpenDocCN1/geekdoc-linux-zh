After you have created your boot disk, you will be asked to configure your modem and mouse. If you decide to do so now, make sure you know which serial ports correspond to them.

When your mouse and modem are configured, you can try out some custom fonts. (Usually, by this time, I want to get done with the installation, so I don't bother.)

To boot your system, Linux has LILO, the Linux Loader. With LILO, you can boot from an OS/2, DOS, Windows 95, or Linux partition. When you reach the Configure LILO menu, do the following steps:

+   1. Start LILO configuration with a new LILO header.
+   2. Add a Linux partition to the LILO config file (choose linux for the label).
+   3. If applicable, add DOS and OS/2 partitions.
+   4. Install LILO.

Don't worry about configuring your network or sending E-mail right now. You can do that later. Do, however, set your time zone.

To make sure your system works properly, press Ctrl+Alt+Del at the same time, as you would in DOS to reboot.

When you see the LILO prompt, type linux to boot Linux. Now you should see the Loading ... and Linux booting other drivers. To make sure you can log in, use the root command without a password—and you're ready to go.

If you're running multiple operating systems, press Ctrl+Alt+Del again, and see whether you can run any other operating system(s) without any conflicts. (More on startup and shutdown in the Chapter 8.) Using Ctrl+Alt+Del at this point won't cause your system any harm that can't be undone.

Congratulations. You've installed your Slackware Linux operating system. You'll see the following prompts to implement your password:

```
bash# passwd
Changing password for root
Enter the new password (minimum of 5, maximum of 8 characters)
Please use a combination of upper and lower case letters and numbers.
New password:
Re-enter new password:
Password changed.
bash#
```

You'll notice your prompt changed from # to bash#. No problem—it simply means you're running the Bash shell. Make sure you pick a good password—something that doesn't make sense to a dictionary password-cracker. Include both numbers and letters but avoid any obvious combinations. Also note that your password does not show up as you type it; anyone who might be looking over your shoulder can't see what characters you're typing.