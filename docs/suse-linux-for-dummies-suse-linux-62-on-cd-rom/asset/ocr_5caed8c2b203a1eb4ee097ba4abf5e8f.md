# 114 Part II: Installing SuSE Linux

# # It Worked!

We congratulate you for getting X Window System working. If you knew all the issues involved in working with PC video hardware, you would think fantastic that the XFree86 developers can get it working at all. Even though XFree86 is freely distributable, you may want to make a donation to their development fund, listed at www.xfree86.org.

If X Server is working and you want it to stop, press Ctrl+Alt+Backspace. You can then log off the root account.

If you want to start X Window System working again, log in to an account and type startx. X Server starts in a few moments. If you are having problems, then you may want to read ahead in the section titled "What Went Wrong"

# # Shutting Down the System

If you are accustomed to MS-DOS or Windows 3.1, it may seem strange to have a section on shutting down the system. After all, shouldn't you turn off the power switch? The answer is no! Linux requires a systematic process to shut down the operating system, after which you can turn off the power switch.

If you have just finished installing the system, you are logged in as systems administrator called root. Follow these steps to shut down the system:

+   1. If X Window System is running, press Ctrl+Alt+Backspace to stop X Window System.

The system returns to character-cell mode, and the # prompt appears. The # prompt tells you that you have the powers of the systems administrator (don't let it go to your head) and that you can shut down the operating system.

+   2. Type shutdown -h now at the prompt.

This tells Linux to halt the operating system now rather than later.

![](bbox=[0.1, 0.809, 0.215, 0.903])

shutdown is a command to Linux. Some commands have options, or flags, that provide additional information about what the command should do. -h means to halt the system, rather than reboot, after it shuts down. -r means to start rebooting after shutdown. now means to start the process of shutting down immediately. Without the now, the shutdown command would hesitate and send warning messages to people still working on the system, telling them that the system is about to be turned off.