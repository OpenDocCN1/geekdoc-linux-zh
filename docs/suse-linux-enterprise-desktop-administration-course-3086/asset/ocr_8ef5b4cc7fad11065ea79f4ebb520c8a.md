# # Objective 1—Perform a SUSE Linux Enterprise Desktop 10 Installation

The SLED 10 installation consists of a base installation phase and a configuration phase. To perform the base installation, do the following:

+   - Boot from the Installation Media
+   - Select the System Language
+   - Select the Installation Mode
+   - Set the Clock and Time Zone
+   - Understand and Change the Installation Settings
+   - Verify Partitioning
+   - Select Software
+   - Start the Installation Process

# ## Boot from the Installation Media

To start the installation process, insert the *SUSE Linux Enterprise Desktop* product DVD into the DVD drive and then reboot the computer to start the installation program.

![](bbox=[0.131, 0.453, 0.318, 0.528])

To start the installation program, your computer needs to be configured to start from a DVD drive. You might need to change the boot drive order in the BIOS setup of your system to boot from the drive.

Consult the manual shipped with your hardware for further information.

When your system has started from the installation CD, your screen should look like Figure 1-1. You can use the arrow keys to select one of the following options:

+   - *Boot from Hard Disk*—Boots the system installed on the hard disk (the system normally booted when the machine is started). This is the default option.
+   - *Installation*—Starts the normal installation process. All modern hardware functions are enabled.
+   - *Installation--ACPI Disabled*—Starts the installation process with ACPI (Advanced Configuration and Power Interface) disabled. If the normal installation fails, the system hardware might not support ACPI. This option allows you to install without ACPI support.
+   - *Installation--Local APIC Disabled*—Starts the installation process with local APIC (Advanced Programmable Interrupt Controller) disabled.
+   - *Installation--Safe Settings*—Starts the installation process with the DMA (Direct Memory Access) mode and any power management functions disabled. Use this option if the installation fails with the other options.
+   - *Rescue System*—Starts the SLED 10 rescue system. If you cannot boot your installed Linux system, you can boot the computer from the DVD (or the first CD if you are using a CD set) and select this option. This starts a minimal Linux system without a graphical user interface to allow experts to access disk partitions for troubleshooting and repairing an installed system.