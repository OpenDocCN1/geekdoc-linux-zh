pended on other options being set? Remember to use the Help buttons beside each kernel option in the configuration interface, making sure that you understand what each option does and what you need to do to make it work right.

When you’re sure you have your settings right, step through the compilation process again and re-install the kernel. Remember to rerun `lilo` so that the changes take effect. Reboot and try again.

Don’t worry, each time you compile a kernel, you’ll get better at it. When you do make a mistake, it’ll be easier to go back and find and fix it.

# PATCHING THE KERNEL

Like any other operating system, Linux gets upgrades to fix bugs, improve performance, and add new features. These upgrades come out in two forms: a complete new kernel release and a patch. The complete new kernel works well for people who don’t have at least one complete kernel already downloaded. For those who do have a complete kernel downloaded, patches are a much better solution because they contain only the changed code.

Think of patches as comparable to a Windows HotFix or service pack. By itself, they’re useless; but when added to an existing version of Windows, you (hopefully) get an improved product.

You can find out about new patches to the kernel at many Internet sites. Your distribution vendor’s Web site is a good place to start; it’ll list not only kernel updates, but patches to other parts of the distribution as well. Another source is the official Linux Kernel Archive at [http://www.kernel.org](http://www.kernel.org/). That’s where we got the complete kernel to use as the installation section’s example.]

In this section, we’ll apply a patch to update our installation of the 2.2.10 kernel to 2.2.11.

# Downloading and Unpacking Patches

Patch files are located in the same directory from which the kernel is downloaded. This applies to each major release of Linux; so the patch to update 2.10 to 2.2.11 is located in the `/pub/linux/kernel/v2.2/` directory of the Linux kernel FTP site. Likewise, the path to take from Linux 2.3.0 to 2.3.1 is located in `/pub/linux/kernel/v2.3/` directory.

Each path filename is prefixed with the term “patch” and suffixed with the Linux version number being installed by the patch. Note that each patch brings Linux up by only one version; thus the `patch-2.2.11` file can only be applied to Linux-2.2.10. If you have Linux-2.2.9 and wish to bring it up to 2.2.11, you’ll need two patches, both `patch-2.2.10` and `patch-2.2.11`.

Patch files are stored on the FTP server in gzip compressed format. In this example, then, we’ll be downloading `patch-2.2.11.gz`.

Once we have the file from the FTP site, move it to the `usrsrc/` directory (assuming that you unpacked the kernel from the preceding section into `usrsrc/linux`). Decompress the patch using the `gzip` command: