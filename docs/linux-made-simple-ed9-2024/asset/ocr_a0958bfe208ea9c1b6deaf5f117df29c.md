isohybrid distro.iso

Now **fdisk** should show it as a hybrid and you can **dd** it to your USB stick.

# # Go slow

**Q** My computer seems to be running with one of its **CPU** cores tied behind its back. What is going on?

**A** The most likely cause is that a particular process is hogging a lot of your resources, and the program to investigate this is called top. Run it in a terminal and it will show you a summary of overall system usage and a list of programs in order of their CPU usage. The third line will show you the overall CPU usages, which will be something like this (on a lightly loaded system):

```
%top(cpu):  0.7 us,  0.2 sy,  0.0 ni, 99.1 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
```

The first three figures show how much of your CPU capacity is being used for user, system and nice tasks. A nice task is one running at a lower priority, so it uses the CPU only when nothing else wants it. The fourth figure is ‘idle’ – the amount of CPU time not being used. If this is close to zero, you now know why your computer is running slowly – look at the list of tasks to see which is eating the most CPU time. If you have a multi-core CPU, pressing **1** switches between showing an overall usage and separate figures for each core. That **wa** (waiting) figure is also significant: it shows how much time the CPU is waiting for I/O and can be high on disk intensive operations. If it is routinely high, you may have a disk problem – either read errors or a nearly full filesystem that has become heavily fragmented.

Look at the memory figure. If memory is full and swap is in use, you will lose performance. The task list is ordered by CPU usage, but you can press **F** to pop up a list of fields. Move the cursor over the field you want to sort on and press **S** followed by **Q**. It sounds fiddly but the window opened by **F** allows for a lot more than changing sort orders. If memory is low, this will help you find the greedy programs.

# # Lost password

**Q** I reinstalled Linux recently and thought I kept the same password, but I cannot log in with it. Is there a way I can find or reset my password?

**A** You can reset your password by booting from a live CD/DVD – either a specific rescue disc like System Rescue CD or your distro’s own disc. The first step is to identify the partition where your distro is installed (this is the root filesystem for your distro; your **home** directory is not needed).

![](bbox=[0.09, 0.68, 0.41, 0.89])

› *Top* gives an overview of resources used by your system as well as a list of the programs using the most.

![](bbox=[0.43, 0.09, 0.8, 0.25])

If you have booted to a graphical desktop, you can browse the available drives, looking at those of a suitable size until you find the one that contains directories such as **bin**, **etc** and **lib**. Once you have the correct partition mounted, say in /mnt/myroot, you can use **chroot** to fix it:

```
sudo chroot /mnt/myroot /bin/bash
```

This changes the root directory to the path you give and runs the command following. So this switches you to the root of your installed system and runs the *Bash* shell as root. You are now inside your installation and can change your password with:

```
passwd yourusername
```

It will ask you for the new password twice and then write it to disk. Press [Ctrl+D] to exit the **chroot**, reboot from your hard disk and you should now be able to log in.

# # Killing windows

**Q** I run some bleeding edge versions of software and occasionally they crash, leaving the window still open. How do I close a window and program like this so that I can run it again?

> “Most distros have a package that installs everything you need to build and install programs.”

**A** For graphical programs, the simplest answer is **xkill**, which is usually installed by default. When you run **xkill**, your mouse pointer changes to a skull-and-crossbones, the next window you click on will be forcibly closed, along with its program, so be careful where you click.

There are also command line alternatives: **kill** takes a process ID as an argument and kills it. **Killall** does the same but works with program names, so be careful if you may have more than one copy of the program running. Both send a TERM signal by default, which asks the program to shut down cleanly. If this fails, add **-KILL** to the arguments to send the more forceful KILL signal:

```
killall -KILL someprogram
```

If you want to use **kill**, there are various ways to find the PID. If the process is using a lot of CPU or memory it will show up in top, and you can kill it from there by pressing **K**. Otherwise, you can **ps**:

```
ps -ef | grep #1 programname
```

The **-fl** options mean you see the full command line, so you can be sure you are killing the right process.

› **Xkill** will kill the first window you click on, and the process behind it, so be careful.

# # Advanced | Troubleshooting