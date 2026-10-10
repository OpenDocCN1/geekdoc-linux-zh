> **CROSS-REFERENCE:** See Chapter 10 for a description of the root user and Chapter 11 for information on how to set up and use other user accounts. Refer to Chapter 14 for suggestions on how to choose a good password. For information on instances where the root user doesn’t have complete control over the system, refer to the descriptions of SELinux (Security-Enhanced Linux) in Chapter 10.

If your desktop did not start, refer to the “Troubleshooting Your Desktop” section at the end of this chapter. Otherwise, continue on to the next section.

# # Why Do I Need a User Login?

If you are working on a PC, and you are the only one using your Linux computer, you may wonder why you need a user account and password. Unlike Windows, Linux (as its predecessor UNIX) was designed from the ground up to be a multisuer system. Here are several good reasons why you should use separate user accounts:

+   - Even as the only person using Linux, you want a user name other than root for running applications and working with files so you don’t change critical system files by mistake during everyday computer use.
+   - If several people are using a Linux system, separate user accounts let you protect your files from being accessed or changed by others.
+   - Networking is probably the best reason for using a Linux system. If you are on a network, a unique user name is useful in many ways. Your user name can be associated with resources on other computers: file systems, application programs, and mailboxes to name a few. Sometimes a root user is not allowed to share resources on remote Linux systems.
+   - Over time, you will probably change personal configuration information associated with your account. For example, you may add aliases, create your own utility programs, or set properties for the applications you use. By gathering this information in one place, it’s easy to move your account or add a new account to another computer in the future.
+   - Keeping all your data files and settings under a home login directory (such as /home/chris) makes it easier to back up the data and restore it later if needed.

# # Getting Familiar with the Desktop

The term desktop refers to the presentation of windows, menus, panels, icons, and other graphical elements on your computer screen. Originally, computer systems such as Linux operated purely in text mode — no mouse, no colors, just commands typed on the screen. Desktops provide a more intuitive way of using your computer.

As with most things in Linux, the desktop is built from a set of interchangeable building blocks. The building blocks of your desktop, to use a car analogy, are: