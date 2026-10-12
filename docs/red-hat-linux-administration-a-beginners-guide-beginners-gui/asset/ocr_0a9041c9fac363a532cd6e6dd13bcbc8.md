Over time, it's been UNIX's command-line options that have given the system its power and flexibility. Casual observers of UNIX gurus are often astounded at the results of a few carefully entered commands. Unfortunately, this power makes UNIX less intuitive to the average user. For this reason, graphical user interfaces (GUIs) have become the de facto standard for many UNIX tools.

More experienced users, however, find that it is difficult for a GUI to present all of the available options. Typically, doing so would make the interface just as complicated as the command-line equivalent. The GUI design is often oversimplified, and experienced users ultimately return to the comprehensive capabilities of the command line.

![](bbox=[0.13, 0.32, 0.23, 0.37])

> Debating the merits of the interfaces is pointless. Each has its weaknesses and benefits. In the end, the person who chooses to master both methods will come out ahead.

Before you begin your study of the command-line interface under Linux, understand that this module is far from an exhaustive resource. Rather than trying to cover all the tools without any depth, this Module describes thoroughly a handful of tools believed to be most critical for day-to-day work.

![](bbox=[0.13, 0.53, 0.23, 0.57])

> For this module, assume that you are logged in, can become the root user, and have started the X Window System environment. (Most of these commands, however, will work without X running, if you log in to the console instead.) You can open a terminal window by going to the Red Hat menu and then selecting System Tools and then Terminal. All of the commands you enter in this module should be typed into the window that appears after the Terminal icon is selected.

# CRITICAL SKILL 6.1 Switching Users: su

Once you have logged in to the system as one user, you need not log out and back in again in order to assume another identity (the root user, for instance). Instead, use the su command to switch. This command has only two command-line parameters, both of which are optional.

Running su without any parameters will automatically try to make you the root user. You'll be prompted for the root password and, if you enter it correctly, will drop down to a root shell. If you are already the root user and want to switch to another ID, you don't need to enter the new password when you use this command.