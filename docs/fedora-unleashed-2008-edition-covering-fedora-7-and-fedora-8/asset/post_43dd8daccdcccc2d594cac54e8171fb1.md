
connect to your system, keep this box enabled so that you know when people are connecting. You should always enter a password, no matter who might connect. VNC, like XDMCP, should not be considered secure over the Internet, or even on untrusted networks.

## Reference

- http://www.openssh.com/—The home page of the OpenSSH implementation of SSH that Fedora Core Linux uses. It is run by the same team as OpenBSD, a secure BSD-based operating system.
- http://www.realvnc.com/—The home page of the team that made VNC at AT&T's Cambridge Research Laboratory. It has since started RealVNC Ltd., a company dedicated to developing and supporting VNC.
- http://www.tightvnc.com/—Here you can find an alternative to VNC called TightVNC that has several key advances over the stock VNC release. The most important feature is that TightVNC can use SSH for encryption, guaranteeing security.
- http://www.nomachine.com/—Another alternative to VNC is in the pipeline, called NX. The free implementation, FreeNX, is under heavy development at the time of writing but promises to work much faster than VNC.

One book on SSH that stands out from the crowd is known as “The Snail Book” because of the picture on the cover. It covers the entire SSH suite and is called *SSH: The Secure Shell* (O’Reilly), ISBN: 0-596-00011-1.

# CHAPTER 16
# Xen

Xen is a powerful new virtualization system that enables you to run multiple operating systems on one computer. If you have ever used virtualization software such as VMware or Virtual PC, you have an idea how Xen works, except that it is faster, more powerful, and, of course, completely free.

This chapter contains an introduction to the world of Xen: how it differs from normal virtualization solutions, how you can install it on your Fedora machine, and how to get it configured to best suit your environment.

## Why Virtualization Is a Smart Idea

The last few years have seen an incredible growth in the market for blade servers—high-performance, low-cost, space-saving servers that can be hooked together to form massive computing networks. These server farms provide a terrific amount of power for a relatively small budget, but the main problem with them is that distributing workload makes idle servers much more likely. For example, server A is a monolithic server: It has four CPUs, 4GB RAM, and so on, and runs both your database and web servers. If your database server is quiet but your web server is overrun with requests, it simply gives more resources to the web server. The downside here is that running multiple servers on one computer is insecure—a hole in your web server (hardly an uncommon thing) would also expose your database server. Now imagine that situation in which there are two servers: one running a database and the other running the web server. In this scenario, the database blade server would stand idle while the web server is swamped with requests.

## IN THIS CHAPTER

- Why Virtualization Is a Smart Idea
- Virtualization Versus Paravirtualization
- How Xen Works
- Installing Xen
- Setting Up Guest Operating Systems
- Runtime Configuration
- Reference

If you think this problem is quite rare, you ought to know that experts estimate that current server farm utilization is as low as 15%, which means that 85% of your computers are likely to be sitting around waiting for something to do. Virtualization allows you to create multiple independent virtual machine (VM) operating systems that run on a single server. If one VM needs more processing power, the server simply allocates it more resources. More importantly, because the VMs are completely isolated from each other—they are literally treated as independent hardware—a security hole in one server cannot affect the others.

Moving your server farm from 15% to 80% or higher utilization either means your users get a much faster and more reliable service, or you suddenly have a huge amount of hardware that you can sell or keep offline until needed. Either way, it is a huge cost savings, which makes virtualization the easiest way to cut your IT budget.

### Virtualization Versus Paravirtualization

The method in which operating systems are kept isolated is quite simple: They really do each get a virtual machine. When you create a new VM, it is allocated a chunk of RAM all to itself, and lives completely self-contained from the outside world. VMware even has a virtual BIOS to complete the illusion. If your VM wants to communicate to other VMs on the same computer, it has to do so over a TCP/IP network connection, just like any other machine. In fact, when you install an operating system on a virtual machine, it cannot even tell that it is a virtual machine because it looks identical to raw hardware.

The problem with this type of virtualization is that it is very slow. For example, if the VM has to access hardware frequently (to save files, show a display, and so on), but of course it cannot access the hardware directly because doing so would interfere with other VMs. Instead, its requests have to be translated and routed to the host operating system (OS), where they are handled. Similarly, if the VM tries to execute any special CPU instructions that would reveal that the VM is actually a virtual machine, the host OS has to stop those instructions and fake the answer so that the VM is not any wiser (a technique known as *binary patching*).

The solution is to move from virtualization to paravirtualization—the technique that Xen uses. Linux is open source, so the Xen developers modified the Linux source code so that Linux becomes aware of its existence as a virtual machine. When the virtual Linux needs access to the hardware, it just asks Xen for permission. The difference is huge: You can expect a normal VM to run at about 50% of the speed of a native machine, whereas a Xen virtual machine can run up to about 95%, simply by removing the need for binary patching and other virtual hacks.

The downside to Xen is that the source code has to be patched, which rules out closed-source operating systems. VMware runs Windows XP on Linux out of the box, but Xen cannot. That said, the new chips from Intel and AMD include virtualization on hardware, which enables Xen to run unmodified Windows at full speed on top of Linux. Without this technology, Xen can use only a modified, open source distribution, such as Linux, NetBSD, or FreeBSD.

## How Xen Works

Xen is actually a very small operating system that has the sole goal of managing the resources of virtual machines. On top of the Xen OS runs what would previously have been called the *host OS*—the main operating system for the machine. Unlike VMware, the host OS (known as *domain 0* or just *dom0* in Xen terminology) is a virtual machine, but has special privileges assigned to it so that it is more responsive.

The domain 0 VM is where you control Xen, and where you start other guest VMs—known as *unprivileged domains* or *domU*. You can start as many as you want, with the only real limit being the amount of RAM in your machine. Because the domU OS is fully aware of its status as a Xen virtual machine, Xen lets you change the amount of RAM in a VM while it’s running, with the exception that you can’t go above the initial allocation of RAM.

Fedora Linux specifies a minimum system requirement of 256MB RAM, which means that if you are to run Fedora on top of Fedora, you need at least 512MB RAM. Keeping in mind that Xen uses a very small amount of RAM for itself, you should ideally have at least 768MB of RAM to be able to run two operating systems side by side at full speed.

Note that if you have tried Xen on old versions of Fedora, you no longer need to disable SELinux to get Xen to work.

## Installing Xen

The first step is to convert your current OS to a virtualized guest OS. This is actually a very easy thing to do because, as discussed, domain 0 has special privileges—such as the capability to access hardware directly. As a result, you do not have to reformat your machine: dom0 reads straight from the disk, uses the graphics card, uses the sound card, and so on.

To get started, go to Applications, Add/Remove Software. From the window that appears, choose List view, and then select the following packages: `kernel-xen`, `vnc`, and `xen`. The `kernel-xen` package provides a Linux kernel that is configured to run on top of Xen without any special privileges, as well as a Linux kernel designed to be used as dom0 so it can access hardware directly. The vnc package is there to make VM management much easier. Finally, the xen package gives you all the tools you need to create and manage virtual machines. Along with these packages, there are several other dependencies that Fedora will automatically resolve for you, so just go ahead and install all the packages.

Because you have installed two new kernels, Fedora updates your Grub boot configuration to make them bootable, but leaves your original, non-Xen kernel as the default. Switch to root and bring up `/boot/grub/grub.conf` in your favorite text editor. Look for the line `“default=2”` and change it to read `“default=0”`. This might vary on your machine—set it to the position of the Xen hypervisor kernel in the `grub.conf` file, remembering that Grub counts from 0 rather than 1. That is, the first OS in the list is considered to be number 0. Note that you should not set the guest kernel as the default because it will *not* boot—it is designed only to be created on top of the hypervisor (dom0).
