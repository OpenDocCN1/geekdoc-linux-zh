
# Chapter 5: Running VMware for the First Time

Launching VMware

VMware's configuration menus

Using the Configuration Wizard

Using the Configuration Editor

If it seems as though I’m trying to get you excited about VMware, it’s because I am. If I’m doing the job right, by now you should be yelling, “Less talking! More VMware!” I’m sure you have the CD for the first OS you want to install in a virtual machine sitting on the desk already.

But haste makes waste—and, more importantly, could make running VMware a hassle. This chapter describes the final piece of the VMware configuration puzzle. Here, you will learn the ins and outs of the VMware configuration and launch program, and then it’s on to Windows and other guest operating systems!

## Launching VMware

This is it. This is what you’ve been waiting for:

- 1. Log in to Linux as the same user account you used to install VMware.
- 2. Start XWindows and open a terminal window.
- 3. At the terminal prompt, enter `/usr/bin/vmware`.
- 4. VMware opens and then tests your display. This process ensures that your X server can support VMware and probes your system for valid screen modes to use in virtual machine guest operating systems. It should only take a moment. Soon after, you will see the VMware screen, shown in Figure 5.1.
- 5. VMware detects that you do not yet have any virtual machines configured and asks you to run the Configuration Wizard or Configuration Editor, using the window shown in Figure 5.2. Although you ultimately want to use the Configuration Wizard VMware invites you to run, for now click Cancel to close this window.

## VMware’s Configuration Menus

VMware’s launch screen is extremely low-frills; once you’ve made it this far, there’s not much to worry about except configuring a virtual machine in VMware’s Configuration Wizard. But there are still some important tools and operations in the launch screen that you should be aware of.

![](img/b2b6702758c230ce537468351fc8af15_76_0.png)

Figure 5.1 The VMware welcome screen.

![](img/b2b6702758c230ce537468351fc8af15_76_1.png)

Figure 5.2 If VMware cannot find any virtual machine configurations, you are prompted to create one.

### File Menu

As in most applications, VMware's File menu manages the files VMware loads and saves, specifically virtual machine configurations:

- New begins a new VMware configuration using the standard VMware Configuration Editor. Some VMware features can only be selected in the Configuration Editor.
- Wizard opens the VMware Configuration Wizard, which is generally friendlier than the Configuration Editor.

![](img/b2b6702758c230ce537468351fc8af15_77_0.png)

Although the Configuration Editor is certainly more powerful than the wizard, you should use the wizard to do the initial setup for any virtual machine you create and then make changes in the editor.

- Open presents you with a dialog box and asks you to select a virtual machine configuration file. Each virtual machine configuration should be in its own directory.
- Open Recent presents you with a short list of recently used virtual machine configurations.
- Instant Restore is used in conjunction with VMware's built-in Suspend function. Instant Restore awakens the virtual machine you most recently suspended to memory or disk.
- Save As allows you to choose a new configuration filename before saving it to disk.
- Exit closes the VMware configuration screen (and closes the virtual machine, if you left it running).

![](img/b2b6702758c230ce537468351fc8af15_77_1.png)

The Power menu not only gives you the virtual machine's virtual toggle switch, but also offers other convenient virtual power management features:

- Power On, only available when you are not running a virtual machine, boots the currently loaded VMware configuration.
- Power Off takes the place of Power On whenever a virtual machine is running.
- Power Reset reboots the virtual machine.

> Whenever possible, use the guest operating system's built-in shutdown sequence before selecting Power Off or Power Reset in VMware. Just as on a physical PC, you could damage the guest operating system's data if you don't.

- Suspend VM is only available when a virtual machine is running. It suspends the current virtual machine to disk (default) or memory. It works even in operating systems that do not support their own suspend feature, although it can take advantage of APM (Advanced Power Management) suspend/restore features as found in most versions of Linux and Windows.
- Resume VM becomes active when a virtual machine has been suspended. It attempts to restore the suspended virtual machine at the exact point you left off.

> You can resume a virtual machine saved to disk at any point—even after quitting VMware or even rebooting Linux. However, a virtual machine saved to memory is lost as soon as you exit VMware.

- Send Ctrl-Alt-Del gives the infamous "three-finger salute" to the guest operating system. In most operating systems, this either starts a reset or (in Windows) opens the Task Manager.

> Why is Send Ctrl-Alt-Del a separate menu item? The feature is actually a carryover from the Windows NT version, which cannot read Ctrl+Alt+Del from the keyboard because of NT's security system. There may be a Linux benefit as well. Although VMware tries to intercept all your keystrokes and send them to the virtual machine instead of Linux, you might not want to hammer away at it and risk sending your host PC into a reset!

- Grab gives the virtual machine control of your mouse and keyboard. In other words, use this when you want to interact with the virtual machine, rather than your Linux host OS.
