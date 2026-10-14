turning off the power could result in the loss or corruption of some of your work.

There is a special shutdown tool the system administrator can use to shut down the computer, as described in Recipe A.2 [Shutting Down the System], page 703. But you can always shut down your system from the console, whether you are logged in or not, by using the special CTRL - ALT - DEL keystroke (also known as the "three-finger salute," a carry-over from the DOS days). This keystroke immediately begins the shutdown process, and then reboots the system. If you cut power to the system before it reboots, you can shut it down in this way.

⇒ To turn off a single user system even when you are not logged in as the administrator, type CTRL - ALT - DEL (press and hold these three keys at once).¹

When you do this, the system will display some messages to the screen as it shuts down; when you see the line, "Rebooting...," it's safe to flip the power switch.

NOTES: You don't want to wait too long after you see this message; if left untouched, the system will reboot and you'll be back to the beginning!

# 2.2 Using Your Account

Linux is a multi-user system, meaning that many users can use one Linux system simultaneously, from different terminals. So to avoid confusion (and to maintain a semblance of privacy), each user's workspace must be kept separate from the others.

Even if a particular Linux system is a stand-alone personal computer with no other terminals physically connected to it, it can be shared by different people at different times, so the separation of user workspace is still a valid issue.

This separation is accomplished by giving each individual user an account on the system. You need an account in order to use the system; with an account you are issued an individual workspace to use, and a unique username that identifies you to the system and to other users. The username is the name that the system (and those who use it) will then forever know you by; it's a single word, in all lowercase letters.

During the installation process, the system administrator should have created an account for you. (The system administrator has a special account

¹ If your keyboard has two ALT and CTRL keys, use the left set of these keys.