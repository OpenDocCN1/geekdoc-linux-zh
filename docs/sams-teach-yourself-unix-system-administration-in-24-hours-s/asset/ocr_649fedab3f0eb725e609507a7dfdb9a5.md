# Answers

+   1. LILO is the Linux Loader, and GRUB is the GRand Unified Boot loader.
+   2. The BIOS gets the system started, then the PRAM is checked for the specific configuration details. One of the most important snippets of information therein is the boot disk, so the next step is switching control of the system to the code in the master boot record.
+   3. Having the disk properly partitioned for multiple operating systems *before installing any of them.*
+   4. That you've set it to a sufficiently large value: The timeout is calculated in tenths of a second, not seconds.
+   5. The GRUB developers fixed the program so that it won't install a bad configuration, so testing the configuration is less critical. You should still proceed with caution nonetheless.

In the next hour, you'll learn about disk quotas, both those that are built in to various Unix flavors, and those you can build yourself with some savvy shell scripts. More importantly, we'll also look at the find command in detail and explore how it can help with many system administration tasks.