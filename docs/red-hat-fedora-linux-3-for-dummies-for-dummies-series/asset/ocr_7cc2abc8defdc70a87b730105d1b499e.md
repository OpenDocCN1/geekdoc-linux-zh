# # Fending off modular rootkits

A *rootkit* is a software program that a hacker installs on your machine and then uses against you and others; the software also includes tools to hide itself from you. Garden-variety rootkits run as regular applications and can be detected with standard tools. Many rootkits (nearly 60 at the time we wrote this book) can be detected with the easy-to-use chkrootkit system. Go to www.chkrootkit.org and download the software by clicking the Latest Source Tarball link (about a page down under “Download”).

One of the newer and more insidious threats is the *modular rootkit*. Modular rootkits insert themselves into your Linux kernel and then control everything on your computer. Because they live in your kernel, you cannot depend on any standard detection tools to ferret them out.

After you employ the good security techniques discussed in this chapter and this book, the best way to avoid modular rootkits is to prevent kernel modules from being loaded. You can download the Linux rootkit source code from kernel.org and compile it as a *monolithic kernel*—that is, compile modules directly into the kernel. Describing how to compile monolithic kernels is beyond the scope of this book, but an alternative method is quite easy to use.

Here's the alternative: You can take advantage of a feature in the 2.6 Linux kernel that Fedora Core 3 uses. The 2.6 kernel and its modules include cryptographic signatures that can be used to prevent non-signed modules from loading. Using this feature greatly reduces the danger of getting infected with modular rootkits.

To prevent unsigned module loading add the enforcemodulesig option to the kernel configuration in /boot/grub/grub.conf. For instance, your grub.conf file should look like the following:

```
title Fedora Core (2.6.8-1.541)
    root (hd0,0)
    kernel /vmlinuz-2.6.8-1.541 ro
    root=LABEL=/ rhgb quiet enforcemodulesig
    initrd /initrd-2.6.8-1.541.img
```

This option will take effect the next time you reboot your computer.

# # Introducing SELinux

The new and powerful Security-Enhanced Linux (SELinux) was designed by the National Security Agency (NSA) to increase computer security (see www.nsa.gov/selinux/). SELinux has recently been added to the Linux kernel. (Adding new functions to the kernel is a difficult process. Only the very best software gets added.)