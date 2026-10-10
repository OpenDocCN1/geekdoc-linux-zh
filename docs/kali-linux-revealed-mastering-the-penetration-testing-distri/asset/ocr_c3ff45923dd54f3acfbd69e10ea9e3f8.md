There are many virtualization tools available for all major operating systems, including VirtualBox®, VMware Workstation®, Xen, KVM, and Hyper-V to name a few. Ultimately, you will use the one that best suits you but we will cover the two most frequently-used in a desktop context: VirtualBox® and VMware Workstation Pro®, both running on Windows 10. If you don’t have corporate policy constraints or personal preference, our recommendation is that you try out VirtualBox first, as it is free, works well, is (mostly) open-source, and is available for most operating systems.

For the next sections, we will assume that you have already installed the appropriate virtualization tool and are familiar with its operation.

# Preliminary Remarks

To fully benefit from virtualization, you should have a CPU with the appropriate virtualization features and they should not be disabled by the BIOS/UEFI. Double check for any “Intel® Virtualization Technology” and/or “Intel® VT-d Feature” options in the Setup screens.

You should also have a 64-bit host operating system, such as amd64 architecture for Debian-based Linux distributions, x86_64 architecture for RedHat-based Linux distributions, and Windows ... 64-bit for Windows.

If you lack any of the prerequisites, either the virtualization tool will not work properly or it will be restricted to running only 32-bit guest operating systems.

Since virtualization tools hook into the host operating system and hardware at a low level, there are often incompatibilities between them. Do not expect these tools to run well at the same time. Also, beware that professional versions of Windows come with Hyper-V installed and enabled, which might interfere with your virtualization tool of choice. To turn it off, execute “Turn windows features on or off” from Windows Settings.