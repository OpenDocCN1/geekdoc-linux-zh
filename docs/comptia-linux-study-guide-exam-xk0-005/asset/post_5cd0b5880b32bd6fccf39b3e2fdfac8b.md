
## Chapter 29 Inspecting Cloud and Virtualization Services

Objective 3.5: Summarize container, cloud, and orchestration concepts

![](img/c0a399aca0d18f8822d714ad0a173123_856_0.png)

When designing and managing various cloud and virtualization system configurations, you need to understand how virtual and physical networks interoperate, the various disk storage choices available, how to automate booting a system, and how you can quickly install Linux distributions on your virtual machines. In addition, you need to be aware of some basic virtual machine creation and management tools. In this chapter, we’ll continue our journey, which started in Chapter 28, into cloud and virtualization topics.

### Focusing on VM Tools

Various virtual machine utilities allow you to create, destroy, boot, shut down, and configure your guest VMs. There are many open source alternatives from which to choose. Some work only at the command line and sometimes are used within shell scripts, whereas others are graphical. In the following sections, we’ll look at a few of these tools.

### Looking at libvirt

A popular virtualization management software collection is the `libvirt` library. This assortment includes the following elements:

- An application programming interface (API) library that is incorporated into several open source VMMs (hypervisors), such as KVM
- A daemon, `libvirtd`, that operates on the VM host system and executes any needed VM guest system management tasks, such as starting and stopping the VM
- Command-line utilities, such as `virt-install` and `virsh`, that operate on the VM host system and are used to control and manage VM guest systems

While typically most command-line utilities that start with `vir` or `virt` employ the `libvirt` library, you can double-check this using the `ldd` command. An example is shown in Listing 29.1 on a Rocky Linux distribution that has hypervisor packages installed.

**Listing 29.1: Checking for `libvirt` using the `ldd` command**

```bash
$ which virsh
/usr/bin/virsh
$
$ ldd /usr/bin/virsh | grep libvirt
libvirt-lxc.so.0 => /lib64/libvirt-lxc.so.0 (0x00007f4a3a10c000)
libvirt-qemu.so.0 => /lib64/libvirt-qemu.so.0 (0x00007f4a39f08000)
libvirt.so.0 => /lib64/libvirt.so.0 (0x00007f4a39934000)
$
```

A primary goal of the `libvirt` project is to provide a single way to manage virtual machines. It supports a number of hypervisors, such as KVM, QEMU, Xen, and VMware ESXi. You can find out more about the `libvirt` project at the `Libvirt.org` website.

### Viewing `virsh`

One handy tool that uses the `libvirt` library is the `virsh` shell. It is a basic shell you can employ to manage your system’s virtual machines.

> **NOTE**
> If you’d like to try out the `virsh` shell, you can obtain it through the `libvirt-client` or `libvirt-clients` package. For older distributions, it may be located in the `libvirt-bin` package. Package installation was covered in Chapter 13, “Governing Software.” Be aware that additional software packages are needed to create virtual machines.

If you have a VMM (hypervisor) product installed, you can employ the `virsh` shell to create, remove, start, stop, and manage your virtual machines. An example of entering and exiting the `virsh` shell is shown in Listing 29.2. Keep in mind that super user privileges are typically needed for shell commands involving virtual machines.

**Listing 29.2: Exploring the `virsh` shell**

```bash
$ virsh
Welcome to virsh, the virtualization interactive terminal.
Type: 'help' for help with commands
'quit' to quit
virsh # exit
$
```

You don’t have to enter the `virsh` shell in order to manage your virtual machines. The various `virsh` commands can be entered directly from the Bash shell, which makes it useful for those who wish to use the commands in shell scripts to automate virtual machine administration. An example of using the `virsh` utility interactively is shown in Listing 29.3.

**Listing 29.3: Using the virsh utility interactively**

```bash
$ virsh help setcpus
NAME
    setcpus - change number of virtual CPUs
SYNOPSIS
    setcpus <domain> <count> [--maximum] [--config]
    [--live] [--current] [--guest] [--hotpluggable]
DESCRIPTION
    Change the number of virtual CPUs in the guest domain.
OPTIONS
    [--domain] <string>    domain name, id or uuid
    [--count] <number>     number of virtual CPUs
    --maximum              set maximum limit on next boot
    --config               affect next boot
    --live                 affect running domain
    --current              affect current domain
    --guest                modify cpu state in the guest
    --hotpluggable         make added cpus hot(un)pluggable
$
```

![](img/c0a399aca0d18f8822d714ad0a173123_859_0.png)

An easier utility than virsh to use for creating virtual machines at the command line is the virt-install utility. It is a Python program and is typically available from either the virtinst or virt-install package, depending on your distribution.

### Managing with Virtual Machine Manager

Not to be confused with a hypervisor (VMM), the Virtual Machine Manager (also called VMM) is a lightweight desktop application for creating and managing virtual machines. It is a Python program available on many distributions that employ a GUI and is obtainable from the virt-manager package.

The Virtual Machine Manager can be initiated from a terminal emulator within the graphical environment via the virt-manager command. The VMM user interface is shown on a Rocky Linux 8 distribution in Figure 29.1.

**FIGURE 29.1 Virtual Machine Manager**

![](img/c0a399aca0d18f8822d714ad0a173123_860_0.png)

You do need to use super user privileges to run the Virtual Machine Manager, and if the `virt-manager` command is not issued from an account with those privileges, it will open a pop-up window asking for the root account password or something similar, depending on the distribution.

One nice feature the Virtual Machine Manager provides through its View menu is performance statistic graphs. In addition, the GUI interface allows modification of guest virtual machines' configurations, such as their virtual networks (virtual network configurations are covered later in this chapter).

![](img/c0a399aca0d18f8822d714ad0a173123_861_0.png)

The Virtual Machine Manager offers, by default, a virtual network computing (VNC) client viewer (`virt-viewer`). Thus, a graphical (desktop environment) console can be attached to any running virtual machine. However, SPICE also can be configured to do the same. VNC and SPICE were covered in Chapter 8, “Comparing GUIs.”

You can view screenshots of the Virtual Machine Manager, read its documentation, and peruse its code at the `Virt-manager.org` website.

### Understanding Bootstrapping

A bootstrap is a small fabric or leather loop on the back of a shoe. Nowadays you use them to help pull a shoe onto your foot by hooking your finger in the loop and tugging. A phrase developed from that little tool, “Pick yourself up by your bootstraps,” which means to recover from a setback without any outside help.

Over time, the computer industry began mimicking that phrase with the terms *bootstrapping* and *booting*. They are often used interchangeably, but typically booting a system refers to powering up a system and having it start via its bootloader code. Bootstrapping a system refers to installing a new system using a configuration file or image of an earlier system installation.

#### Booting with Shell Scripts

Whether you are creating guest virtual machines in the cloud or on your own local host machine, there are various ways to get them booted. Starting a few VMs via a GUI is not too terribly difficult, but if your company employs hundreds of virtual machines, you need to consider automating the process.

Using shell scripts for booting virtual machines is typically a build-your-own approach, though there are many examples on the Internet. It works best for booting guest virtual machines on a company-controlled host machine.

![](img/c0a399aca0d18f8822d714ad0a173123_861_1.png)

If you prefer not to start from scratch, take a look at GitHub for available scripts. One popular project, which has several forks, is `http://github.com/gjtorres/kvm-install-vm`.

You can create configuration files for your various virtual machines and read them into the shell script(s) for booting as needed. The guest can be booted, when the host system starts, at predetermined times, or on demand. This is a flexible approach that allows a great deal of customization.
