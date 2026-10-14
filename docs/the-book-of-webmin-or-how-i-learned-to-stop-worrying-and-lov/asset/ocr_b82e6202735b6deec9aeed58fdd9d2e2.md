![](bbox=[0.25, 0.13, 0.72, 0.48])

Figure 14-4: GRUB Boot Loader

NOTE When you click a kernel or OS icon or the Edit Global Options button, Webmin runs GRUB to obtain the details for that kernel or the global configuration details. This process can take 30 seconds or more, because GRUB scans the system for disks and reads in the current boot configuration details.

# Global Options

The Global Options page provides access to the options that will apply to all bootable kernels and operating systems, including the kernel to boot by default, password options, and boot timeout (Figure 14-5).

![](bbox=[0.25, 0.79, 0.7, 0.86])

Figure 14-5: Global Options

# Default boot option

This option allows you to specify the kernel or operating system that will be booted by default, if nothing is selected by the user from the boot menu. This option corresponds to the default directive in the grub.conf configuration file.

# Fallback boot option

If the user-selected or default boot option fails because GRUB cannot locate the necessary file, this specifies the kernel or OS that GRUB should attempt to boot. This option correlates to the fallback directive.