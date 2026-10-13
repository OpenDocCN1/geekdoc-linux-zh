# Becoming root, When You Must

You have to log in as `root` to perform the system administration tasks. The `root` user is the superuser and the only account with all the privileges needed to do anything in the system.

Common wisdom says you should **not** normally log in as root. When you’re root, all it takes is one misstep, and you can easily delete all the files — especially when you’re typing commands. Take, for example, the command `rm *.html` that you’re typing to delete all files that have the `.html` extension. What if you accidentally press the spacebar after the asterisk (*)? The shell takes the command to be `rm * .html` and — because * matches any filename — deletes everything in the current directory. Seems implausible until it happens to you!

If you’re logged in as a normal user, how do you do any system administration chores? Well, you become root for the time being. If you’re working at a terminal window or text-mode console, type

```
su -
```

Then enter the root password in response to the prompt. From this point on, you’re root. Do whatever you have to do. To return to your usual self, type

```
exit
```

That’s it! It’s that easy.

# Resetting a Forgotten root Password

To perform system administration tasks, you have to know the root password. What happens if you forget the root password? Not to worry: Just reboot the PC and you can reset the root password by following these steps:

+   1. **Reboot the PC** (select Reboot as you log out of the GUI screen) or power up as usual.
+   
+      If you have more than one operating system installed, use the arrow key to select SUSE Linux as your operating system. Soon you see the graphical boot screen that shows the names of the operating systems you can boot.
+   
+   2. **Press E twice.**
+   
+      You’ll see a text line showing the GRUB command line for the booting the Linux kernel.