
If you can’t reach the computers that your DNS server is serving by name or IP address, you should make sure that each client’s address records are correct. You can also try to ping each client and server computer using the full hostname or IP address.

## Getting More Information about BIND

For details on many other BIND options that I don’t describe in this chapter, you can refer to the following:

- `/usr/share/doc/bind-9*/arm` — Contains HTML and XML versions of the BIND 9 Administrator Reference Manual.
- Man pages — Type the `man` command, following it with `named` or `named.conf`. These man pages contain terse descriptions of options and variables that relate to the `named` daemon and `named.conf` file, respectively.
- Internet Software Consortium (http://www.isc.org/software/bind) — The ISC Web site contains information and downloads related to BIND. On this site, find links to BIND mailing lists, security advisories relating to BIND, and BIND history.

## Summary

The choice to connect your Fedora server to the Internet isn’t one to take lightly. If the server is critical to your business and support for the server is too much for you to handle, you should consider handing your server over to a hosting provider.

If you do decide to expose your Fedora server to the Internet to offer Web, FTP, mail, or other types of services, you should carefully consider the security implications and prepare for them. By using Linux features that I describe in other parts of this book, you can create firewalls, monitor log files, and track changes to system files to protect your computers.

One way of controlling the public exposure of your servers is to obtain a domain name and configure your own Domain Name System (DNS) server. With Fedora, you will most likely use BIND (which is on the DVD that comes with this book). You can set up your DNS server to resolve hostnames to IP addresses for clients that request the information from the Internet, as well as to the users on your local, private LAN.

# Chapter 25

## Setting Up Virtual Servers

### In This Chapter

- Preparing for virtualization
- Creating virtual guests
- Managing virtual guests
- Working with virtualization commands

The future of virtualization for Fedora can be spelled in three letters: KVM. The Kernel Virtualization Module (KVM) project drives development of a range of virtualization features that have made their way into Fedora. Instead of requiring a special kernel or proprietary software, as other virtualization solutions do, KVM is built right into the standard kernel that comes with Fedora.

Although virtualization features such as Xen are being phased out, some of the same tools you may have used in earlier versions of Fedora can still be used, but with KVM on the back end. For example, you can still create and manage virtual guests with the Virtual Machine Manager (`virt-manager`) GUI and launch and manage guests using QEMU tools.

Using virtualization, you can have multiple operating systems running on your Fedora system. Those systems can be other Linux systems, Windows systems, or simply multiple instances of Fedora. As demands for those guests change over time, you can configure them to migrate to different machines on-the-fly, so they can instantly start running on other machines.

There are both GUI and command-line tools to create your virtual guests. You can create virtual guests by launching installers for your Linux system of choice and clicking through the install or you can use kickstart files to fully automate the install process. Using operating system images on CD or DVD, or from your file system, you can boot up installers or simply boot and run those operating systems as live CDs.

Figure 25-1 shows a Fedora desktop with the Virtual Machine Manager displayed for managing several guest operating systems. Installed versions of Fedora, Red Hat Enterprise Linux, and Ubuntu are shown running in separate windows. A live CD version of Linux (Puppy Linux) is running directly from a live CD:

![](img/c78bdcb5b7842a0d73dcc98921f872a2_927_0.png)

Figure 25-1: Use Virtual Machine Manager to manage multiple guest systems from a Fedora desktop.

This chapter describes KVM technology and how you can use it to run virtualized operating systems within your Fedora system.

## Preparing for Virtualization

Before you start using KVM, you should understand the extra demands that are put on your system by running guest virtual machines. In particular, you should consider if your computer has enough resources to run virtual guests, check that all the packages you need are installed, and make sure that the necessary services are running.

### Checking computer resources for virtualization

When you run a guest virtual operating system, keep in mind that each instance might consume the same, or nearly the same, computing resources that the host system consumes. In other words, you must have enough processing power, disk space, and memory (RAM) available for all the guests you are running. Here are some things to check:

- **Memory** — Although some can run on less, most modern operating systems run best on at least 512M of RAM. So make sure that you have that much available for your host system, as well as for each guest you are running.
- **Storage** — You must check the disk space requirements for the operating systems you plan to install on your host computer (plus the applications you are installing with them). That storage area can come from a large raw file, a disk partition, logical volume, or one of several different storage file formats. Storage images such as qcow or qcow2 have the advantage of being able to only consume space from your hard disk as the guest requires it. With inexpensive disk space these days, it’s quite normal to create virtual guests with between 4GB and 8GB of disk space.

If your computer does not support hardware virtualization, KVM will rely on QEMU’s software emulation, which can be slow. If your guest operating system supports Xen paravirtualization, it is recommended that you use the Xen hypervisor instead of KVM. Once you have installed your guest virtual machines, you can improve their performance even further by installing paravirtualized Xen or KVM drivers in the guest for storage and network controllers.

Hardware virtualization is enabled by your computer via the BIOS. You can verify that hardware virtualization is available to Fedora by looking for the `svm` or `vmx` flags in `/proc/cpuinfo`. The rest of these instructions assume you are using KVM with hardware virtualization enabled.

### Installing KVM packages

If you are starting with a fresh install of Fedora, you may not have all the packages installed yet that you need to do virtualization. To begin setting up the current Fedora to use KVM, I started by installing the Fedora GNOME Live CD to the hard disk. Then I proceeded to install the Virtualization package group as follows:

```bash
# yum groupinstall Virtualization
```

This installed the following packages, along with about two dozen other packages needed to meet dependencies:

- **libvirt** — Contains the libvirt application programming interface (API) for abstracting away differences between Xen, KVM, and other virtualization technologies.
- **qemu-kvm** — Contains KVM components associated with QEMU utilities.
- **python-virtinst** — Contains commands such as `virt-install` (to create and manage virtual guests), `virt-convert` (to convert VMs into different formats), `virt-image` (to create VMs from image descriptors), and `virt-clone` (to create clone VMs from existing disk images).
- **virt-manager** — Contains the virt-manager Virtual Machine Manager application. It is used to start, stop, and otherwise manage virtual guest operating systems. It also can display summary information and statistics about your guest VMs.
- **virt-viewer** — Contains the virt-viewer Virtual Machine Viewer graphical client, which is used to connect to virtual machines via a VNC interface.
