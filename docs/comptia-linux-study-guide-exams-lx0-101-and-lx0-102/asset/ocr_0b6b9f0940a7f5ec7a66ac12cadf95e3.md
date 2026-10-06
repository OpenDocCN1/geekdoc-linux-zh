The fact that Microsoft is requiring use of a firmware feature known as Secure Boot is likely to have an impact on Linux boot loaders in 2012 and 2013. With Secure Boot enabled, an EFI-based computer will launch a boot loader only if it's cryptographically signed with a key whose counterpart is stored in the firmware. The goal is to make it harder for malware authors to take over a computer by inserting their programs early in the boot process. The problem from a Linux perspective is that use of Secure Boot requires the signing of a Linux loader with its key (since it's the only one's guaranteed to be on most computers), the addition of a distribution-specific or locally generated key to the computer's firmware, or disabling Secure Boot. Fedora has announced that it will use its new boot loader, in conjunction with a signed version of GRUB, to launch Fedora 18 on EFI-based computers; and Ubuntu has announced that it will work with computer manufacturers to add its own key to computers and use its own signed boot loader. In practice, though, you may need to disable Secure Boot or generate your own key to boot an arbitrary Linux distribution or a custom-built kernel.

# Real World Scenario

# Fixing a Damaged Boot Loader Installation

Linux systems sometimes become unstable because the boot loader has been damaged. You can reinstall GRUB if you can manage to boot your system, but of course this is a catch-22. Most Linux distributions provide a way to resolve this problem by enabling you to boot the computer even if the on-disk boot isn't working. Try booting the installation disc you used to boot you, then you can use grub-install to reinstall GRUB from the hard disk. Alternatively, once the system is booted, the installation disc may provide a recovery option that will help to automatically or semi-automatically restore a broken system.

If your distribution's install disc isn't helpful, you can try Super GRUB (http://www.supergrub.org/), which is a bootable disc with a variety of options to locate and use the GRUB configuration file on your hard disk. If Super GRUB can find your GRUB configuration file, you can boot using it and then re-install GRUB to your hard disk.

If all else fails, you may be able to use GRUB's interactive features to locate and boot a kernel. Doing so, however, can be frustrating; a single typo can produce a failure to boot.

# Understanding the Boot Process

Any time you modify your computer boots, the possibility exists that you won't get the results you expect. In these cases, it's useful to know where you can turn for more information about what is happening during startup.