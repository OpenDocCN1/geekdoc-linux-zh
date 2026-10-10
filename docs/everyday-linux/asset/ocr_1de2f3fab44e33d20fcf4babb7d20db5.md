In the terminal screen, type in su. An error message will appear if you didn't properly add yourself to the wheel group. Otherwise, a prompt comes up, and it will look something like this: `password:`. Type in the root password.

You know that you have become root when the ending dollar sign in your prompt changes to a pound sign (#). When you have become root, you can run programs that you could not otherwise. Linuxconf, for instance, is restricted to root only. Type in “linuxconf” in the terminal window, and the linuxconf screen will appear.

You might notice that it looks differently than the rest of your user windows. This is because GNOME and Enlightenment think that you are the root user, and load the preference settings used by root. This includes the desktop theme. If you prefer to use the forest green desktop theme, but root uses the cheese theme, programs run by root will appear using the cheese theme.

You can quit linuxconf now. We don't have a reason to have it open for the moment. This is just an example of how using the su command makes life a little easier. You no longer need to log out of your account, log in to the root account, and fix a problem. Now you can simply use su to fix the problem. This is particularly useful if you administer a larger system with many users.

# Making Upgrades to Your System

As with most systems, you will want to make both software and hardware upgrades to your system. You might find that you need a new hard drive, or that a new version of the GIMP is available. Perhaps your version of StarOffice just became obsolete. Or maybe your graphics card was accidentally fried during a thunderstorm. Myriad reasons to upgrade your system assist.

# Hardware Upgrades

Windows9x pioneered the concept of “plug-and-play” devices. In other words, Windows would detect when a new plug-and-play device was attached to the system, find out what kind of device it was, and install the necessary drivers for it.

Linux has also implemented something similar in recent versions. When you boot into Linux, it will search for new hardware. This is known as a hardware detect process. It's not as refined as the Windows version, but it will pick up new hardware. For instance, when I installed a new Zip drive on my computer, it