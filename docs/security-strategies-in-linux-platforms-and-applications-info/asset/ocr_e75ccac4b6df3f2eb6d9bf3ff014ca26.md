# CHAPTER 10 | Kernel Risk Mitigation

# 291

As the developers behind Linux distributions can't possibly test all configurations, it's up to you to test distribution-specific kernel updates in production.
The standard command to update packages on Ubuntu systems is apt-get update. By default, it excludes later versions of the Linux kernel from an update.

On the other hand, the standard command to update packages on Red Hat systems is yum update. It does not exclude later versions of the Linux kernel unless the --exclude=kernel-* switch is included in the command:

```
# yum update --exclude=kernel-*
```

For more information on the apt-get and yum update commands, see Chapter 11.

# Installing an Updated Kernel

When implementing a new kernel, be careful. Make sure to use appropriate install commands and switches with the package-management commands for your distribution. Ensures that the existing kernel remains in place, still available to boot local systems if the updated kernel does not work for whatever reason.

In contrast, if you upgrade a kernel, the process overwrites any existing kernel. If the new kernel doesn't work for you, you'll have to go through a rescue process to reinstall the older working kernel.

There are two basic methods to install an updated kernel. The first method relates to update tools such as yum or apt-get to download and install kernels from existing repositories on remote systems.

On Ubuntu systems, you can run the apt-get install command with the name of the updated kernel. If you want to install the latest version of the kernel, you could specify the appropriate meta-package shown in Table 10-1. For example, the following command installs the latest version of the Ubuntu kernel customized for virtual machines:

```
# apt-get install linux-image-virtual
```

In the same fashion, you can use the name of the Red Hat kernel to install the latest version of that kernel: for example, the following command installs the latest version of the Xen kernel:

```
# yum install kernel-xen
```

Alternatively, if you've downloaded the actual updated kernel package, you can use the rpm or dkg commands. You should already be familiar with the details of these commands; in both cases, the -i switch installs the target package.

Binary kernel packages built by the developers of Linux distributions should automatically update appropriate bootloader files such as /etc/grio or /boot/menu.list. If properly updated, these files should include stanzas for both the current and the new kernel. If you set up custom features for an existing kernel in the bootloader, you may need to modify the stanza for the new kernel to include those same messages.

> Starting with Red Hat Enterprise Linux 6, Red Hat will no longer support Xen, nor will it include a Xen kernel in release.

![](bbox=[0.435, 0.635, 0.935, 0.935])

# Kernel Risk Mitigation