# # CHAPTER 2. SECURITY TIPS FOR INSTALLATION

Security begins with the first time you put that CD or DVD into your disk drive to install Red Hat Enterprise Linux 7. Configuring your system securely from the beginning makes it easier to implement additional security settings later.

# ## 2.1. SECURING BIOS

Password protection for the BIOS (or BIOS equivalent) and the boot loader can prevent unauthorized users who have physical access to systems from booting using removable media or obtaining root privileges through single user mode. The security measures you should take to protect against such attacks depends both on the sensitivity of the information on the workstation and the location of the machine.

For example, if a machine is used in a trade show and contains no sensitive information, then it may not be critical to prevent such attacks. However, if an employee's laptop with private, unencrypted SSH keys for the corporate network is left unattended at that same trade show, it could lead to a major security breach with ramifications for the entire company.

If the workstation is located in a place where only authorized or trusted people have access, however, then securing the BIOS or the boot loader may not be necessary.

# ### 2.1.1. BIOS Passwords

The two primary reasons for password protecting the BIOS of a computer are[2]:

+   1. *Preventing Changes to BIOS Settings* – If an intruder has access to the BIOS, they can set it to boot from a CD-ROM or a flash drive. This makes it possible for them to enter rescue mode or single user mode, which in turn allows them to start arbitrary processes on the system or copy sensitive data.
+   2. *Preventing System Booting* – Some BIOSes allow password protection of the boot process. When activated, an attacker is forced to enter a password before the BIOS launches the boot loader.

Because the methods for setting a BIOS password vary between computer manufacturers, consult the computer's manual for specific instructions.

If you forget the BIOS password, it can either be reset with jumpers on the motherboard or by disconnecting the CMOS battery. For this reason, it is good practice to lock the computer case if possible. However, consult the manual for the computer or motherboard before attempting to disconnect the CMOS battery.

# #### 2.1.1.1. Securing Non-BIOS-based Systems

Other systems and architectures use different programs to perform low-level tasks roughly equivalent to those of the BIOS on x86 systems. For example, the *Unified Extensible Firmware Interface (UEFI)* shell.

For instructions on password protecting BIOS-like programs, see the manufacturer's instructions.

# ## 2.2. PARTITIONING THE DISK

Red Hat recommends creating separate partitions for the `/boot`, `/.` /home/tmp, and `/var/tmp`/ directories. The reasons for each are different, and we will address each partition.