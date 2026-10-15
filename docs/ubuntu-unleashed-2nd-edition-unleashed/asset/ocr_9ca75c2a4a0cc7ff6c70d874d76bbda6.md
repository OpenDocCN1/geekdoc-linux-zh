them to boot the system. Worthy of a chapter all its own, the GRUB documentation is extensive: In addition to info grub (the info system is similar to the man system for documentation), the GRUB documents contain a tutorial worth reading. The GRUB boot loader is shown in Figure 17.5.

![](bbox=[0.049, 0.188, 0.624, 0.428])

**FIGURE 17.5**  The GRUB boot loader gives you incredible flexibility in booting even unfamiliar systems.

# Using the Recovery Facility

As your computer starts, Ubuntu will show a message prompting you to press Escape to see the GRUB menu. If you do that, you’ll see a list of bootable operating systems, which will include Recovery Mode options for your Ubuntu install. If you boot into recovery mode, you’ll get automatic root access to your machine where can fix your problems safely.

Alternatively, you can insert your Ubuntu installation disc and use the recovery mode from there. Keep in mind that these recovery modes are designed to be text-only systems for serious system recovery purposes; don’t expect them to be hand-held, and don’t expect much in the way of ease of use!

# Relevant Ubuntu Commands

The following commands are useful in performing backup, recovery, and restore operations in Ubuntu:

+   - `dump`—Amanda is a network-based backup system, consisting of 18 separate commands, for use with Linux.
+   - `ark`—A KDE desktop GUI archiving utility.
+   - `cp`—The copy command.
+   - `scp`—The secure shell copy command.
+   - `cpio`—A data archive utility.