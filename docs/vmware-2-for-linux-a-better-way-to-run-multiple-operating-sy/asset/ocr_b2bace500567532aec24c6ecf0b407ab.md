If it seems as though I’m trying to get you excited about VMware, it’s because I am. If I’m doing the job right, by now you should be yelling, “Less talking! More VMware!” I’m sure you have the CD for the first OS you want to install in a virtual machine sitting on the desk already.

But haste makes waste—and, more importantly, could make running VMware a hassle. This chapter describes the final piece of the VMware configuration puzzle. Here, you will learn the ins and outs of the VMware configuration and launch program, and then it’s on to Windows and other guest operating systems!

# Launching VMware

This is it. This is what you’ve been waiting for:

+   1. Log in to Linux as the same user account you used to install VMware.
+   2. Start XWindows and open a terminal window.
+   3. At the terminal prompt, enter `/usr/bin/vmware`.
+   4. VMware opens and then tests your display. This process ensures that your X server can support VMware and probes your system for valid screen modes to use in virtual machine guest operating systems. It should only take a moment. Soon after, you will see the VMware screen, shown in Figure 5.1.
+   5. VMware detects that you do not yet have any virtual machines configured and asks you to run the Configuration Wizard or Configuration Editor, using the window shown in Figure 5.2. Although you ultimately want to use the Configuration Wizard VMware invites you to run, for now click Cancel to close this window.

# VMware’s Configuration Menus

VMware’s launch screen is extremely low-frills; once you’ve made it this far, there’s not much to worry about except configuring a virtual machine in VMware’s Configuration Wizard. But there are still some important tools and operations in the launch screen that you should be aware of.