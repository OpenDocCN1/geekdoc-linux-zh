# 494 Upgrading with a Kernel RPM

# Upgrading with a Kernel RPM

Fedora Core software updates, including new versions of kernels, come in the form of RPM files. To download and install the kernel RPMs, follow these steps:

+   1. Use a Web server to download the kernel RPM files from a Fedora Core download site (I explain the details in the next section).

+   2. If you want to rebuild the kernel, you have to download the kernel-source RPM corresponding to the new version of the kernel.

+   3. Install the RPMs by using the `rpm -i` command.

+   4. Create a new, initial RAM disk by running the `/sbin/mkinitrd` command.

+   5. Reconfigure GRUB to boot the new kernel.

+   6. Try out the new kernel by rebooting the system.

I further describe these steps in the next few sections.

# Downloading new kernel RPMs

Fedora Core software updates are distributed in the form of RPM — packages — from one of the mirror sites listed at `fedora.redhat.com/download/mirrors.html`. The updates are organized in directories according to Fedora Core 1 for 32-bit Intel x86 systems reside in the `fedora/linux/core/updates/1/386/` directory (for Fedora Core 2 updates, replace 1 with 2 in that pathname). Use a Web browser as Mozilla to visit a mirror site and download any kernel RPMs available at that site. Another way to get the new kernel RPM is through the normal update process Up2date or Yum (see Chapter 4 of this minibook for how to use Up2date and Yum).

# Installing the kernel RPMs

To install the kernel and the modules, follow these steps:

+   1. Log in as `root`.

+   2. Use the `cd` command to change the directory to where the RPM files located (the ones you download from a Fedora Core download server).

+   3. Type the following command to install the kernel RPM:

```
rpm -ivh kernel*.rpm
```