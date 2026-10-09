# LAB 30

# Change Runlevels / Boot Targets and Shutdown or Reboot System: Runlevels and Boot Targets

**Lab Objective:**
Learn how to set and change Linux runlevels and boot targets.

**Lab Purpose:**
The standard Linux *runlevels* are as follows:

+   - 0: Halt
+   - 1 (or S): Single-user mode
+   - 2: Multi-user mode, no networking
+   - 3: Multi-user mode, with networking
+   - 4: Unused, or runlevel 3 + display manager
+   - 5: Unused, or runlevel 3 + display manager
+   - 6: Reboot

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

# Lab Walkthrough:

# Task 1:

Make sure all of your work is saved. Then, you will enter single-user mode (rescue mode) from the Terminal:

```
sudo telinit 1
```

You will be greeted with a root command prompt—this is the original Linux! As hinted by the name, this mode is typically used for rescue operations. If you ever forget your root password (and the root partition isn’t encrypted), this is how you could reset it.