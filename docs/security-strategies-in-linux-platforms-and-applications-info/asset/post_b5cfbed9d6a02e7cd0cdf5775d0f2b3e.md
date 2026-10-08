
# PART 2 | Layered Security and Linux

## Configure TrustedGRUB

If you want to configure a boot loader that takes advantage of TPM chip on the local system, consider TrustedGRUB. Properly configured, it can become a part of the so-called chain of trust that verifies important parts of the boot process. TrustedGRUB isn't available as a regular package for Red Hat Enterprise Linux 5 or Ubuntu Server Edition.

However, as early of 2010, TrustedGRUB is available directly from its developers at sourceforge.net/projects/trustedgrub/. IBM documents contain an installation process using this software at http://publish.ibm.com/infocenter/linuxinfo/v3r0mol/index.jsp. Before you make any changes, be sure to back up the boot loader as suggested earlier.

The following steps implement TrustedGRUB on a server system with Red Enterprise Linux 5. Some of the associated packages to compile this package will be removed later to prevent their use by black-hat hackers. Some of the scripts and compilation commands shown can take a few minutes (or more). Similar methods will work on other Linux distributions:

- 1. Download the latest available version of TrustedGRUB from SourceForge project area at the aforementioned http://sourceforge.net Web site. The following assumes that the package has a tar .gz compression. Such packages are colloquially known as tarballs.

- 2. Unpack and uncompress the noted package. For example, in this case, the tar xzf TrustedGRUB-1.1.4.tar.gz command will unpack and uncompress the noted archive. The files are loaded into a directory of the same name.

- 3. Run the build_grub.sh script in the unpacked subdirectory. If you see an error message related to automake and autoconf, install the automake, autoconf, and gcc packages, along with dependencies. (If you're installing these packages on a baseline host, you'll want to remove them later, as they could help a black-hat hacker create more dangerous malware).

- 4. Navigate to a second-level TrustedGRUB subdirectory. If you downloaded the noted tarball in the root user's home directory, that'll be /root/TrustedGRUB-1.1.4/TrustedGRUB-1.1.4/directory. Review the INSTALL text file in that directory. Any instructions you see supersede any directions that follow.

- 5. Run the ./configure command to set up the code that has been unpacked. Run the make and install commands to compile and install code.

- 6. Now you're ready to replace key files in the legacy GRUB boot loader. Assuming your backup is in order, this should not intimidate you. In the /boot/grub/ directory, delete the stage1, stage2 and *.5 files in that directory.

- 7. Navigate to the second level TrustedGRUB subdirectory. Use the following commands to replace the boot loader files that were deleted:

```
# cp stage1/stage1 /boot/grub/
# cp stage2/stage2 /boot/grub/
```

# CHAPTER 3 | Basic Security: Facilities Through the Boot Process

8. To implement these changes, run commands at the GRUB command prompt. The commands that follow assume that the /boot directory is mounted on the first hard drive, on the first partition:

```
# grub
grub> root (hd0,0)
grub> setup (hd0)
grub> quit
```

You should see messages associated with messages related to the stage I and stage 2 boot loaders. Do not be concerned about messages related to the stage 1.5 boot loader. Also, if the /boot directory were mounted on the second hard drive, on the third partition, the commands at the grub> prompt would be (hd1,2) and setup (hd1).

9. The system should now be ready for a reboot. Have your backups in order and a rescue/recovery disk or a live CD ready in things don't work.

At some point in the future, it will be easier to make TrustedGRUB part of the chain of trust verified by a TPM chip on the system motherboard. At that time, the packages should be available in open source repositories, ready for standard installation on enterprise distributions such as those released by Red Hat and Ubuntu.

The menu should not look much different from a regular traditional GRUB menu. It also retains options from the traditional GRUB configuration file, /boot/grub/grub.conf. But with TrustedGRUB and a TPM, you'll have one more check on the integrity of the operating system that booted.

## Challenges with a Standard Kernel

If you're running Linux on desktop, a standard kernel may include a number of server-related features that you don't need and may never use. In the same fashion, if you're running Linux on the server, a standard kernel may include a number of desktop-related features that you don't need and may never use. For these reasons, Red Hat, Ubuntu, and a number of other Linux distributions include somewhat customized kernels.

Questions with Standard Kernels in this section are multifold:

- What kernels can be installed on your system?
- What kernel is best for your needs?
- When do you consider a different kernel?

Chapter 10 addresses these questions in more detail. It also includes a number of follow-up questions, such as when to install a newer kernel for more security, when to use the stock kernel, and when to build your own secure kernel.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_98_0.png)

One common requirement is different kernels for different architectures. In other words, if a Linux distribution supports a CPU, it should have built a kernel customized for that CPU. So generally, the developers of a distribution will build kernels at least for regular Intel/AMD 32-bit and 64-bit systems. The kernel file names for these generic CPUs may seem specific to Intel or AMD, they generally can be used on CPUs from either company. For example, administrators who prefer Ubuntu and their 64-bit system may install a kernel such as linux-server_2.6.31.14.27_amd64.deb on that system.

This interchangeability may go further. For example, multi-core systems can work with both 32-bit and 64-bit kernels. However, this interchangeability may break down with other CPUs. For example, kernels designed for Intel Itanium 64-bit systems can only work on those systems. If you're looking for a generic kernel, consider the 32-bit Linux kernel. It's designed to work with more architectures than any other kernel.

> NOTE Red Hat has decided it will not support Itanium 64-bit systems starting with its Red Hat 6 release.

## Standard Virtual Machine Kernels

Some special configurations may require different kernels. For example, the Xen virtual machine monitor requires a special Linux kernel. That kernel is installed on both the host and the guest virtual machine.

Perhaps the biggest advantage is the kernel customized to work as a virtual machine. Because it takes to simulate different hardware components, fewer options are configured for virtual machines. That makes it possible to remove or disable modules for a great majority of existing hardware. For example, Ubuntu has created a Just Enough Operating System (jeOS) kernel optimized for VMware and KVM-based virtual machines. Such kernels can work with a relatively small footprint; Ubuntu virtual machine kernels have documented minimum RAM requirement of 128 MB.

## Limits on Standard Kernels

Although there are standard kernels built for different architectures and functions, standard kernels released for a distribution still have to work with a wide variety of hardware and software. Sure, server kernels do not need to be optimized for the GUI, desktop kernels generally do not need to be optimized for databases or file servers.

Security is another limitation on standard kernels. For example, the installation of a server-optimized kernel on a desktop system can increase security risks. A black-hat hacker could use features in the server kernel to attack other systems. While installing a desktop-optimized kernel on a server system may be less of a risk, it still doesn't work as well. For example, the server kernel for one distribution is designed to address 64 GB of RAM—lot more than the desktop version of the kernel, which is designed to address 4 GB of RAM.
