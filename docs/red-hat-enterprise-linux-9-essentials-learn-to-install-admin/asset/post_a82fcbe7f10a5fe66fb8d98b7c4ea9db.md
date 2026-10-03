
rather than kvm_intel.

The installation process should also have configured the libvirtd daemon to run in the background. Once again, using a terminal window, run the following command to ensure libvirtd is running:

```
# systemctl status libvirtd
  libvirtd.service - Virtualization daemon
    Loaded: loaded (/usr/lib/systemd/system/libvirtd.service; enabled; vendor preset: enabled)
    Active: active (running) since Wed 2019-03-06 14:41:22 EST; 3min 54s ago
```

If the process is not running, it may be started as follows:

```
# systemctl enable --now libvirtd
# systemctl start libvirtd
```

If the desktop environment is available, run the virt-manager tool by selecting Activities and entering “virt” into the search box. When the Virtual Machine Manager icon appears, click it to launch it. When loaded, the manager should appear as illustrated in the following figure:

![](img/be1f159c3cc937d7b264dc5b134856dc_181_0.png)

Figure 21-1

If the QEMU/KVM entry is not listed, select the File -> Add Connection menu option and, in the resulting dialog, select the QEMU/KVM Hypervisor before clicking on the Connect button:

![](img/be1f159c3cc937d7b264dc5b134856dc_181_1.png)

Figure 21-2

If the manager is not currently connected to the virtualization processes, right-click on the entry listed and select Connect from the popup menu.

## 21.5 Summary

KVM is a Type-1 hypervisor virtualization solution that implements full virtualization with support for unmodified guest operating systems using Intel VT and AMD-V hardware virtualization support. It is the default virtualization solution bundled with RHEL 9 and can be installed quickly and easily on any RHEL 9 system with appropriate processor support. With KVM support installed and enabled, the following chapters will outline some options for installing and managing virtual machines on a RHEL 9 host.

## Chapter 22

## 22. Creating KVM Virtual Machines on RHEL 9 using Cockpit

KVM-based virtual machines can easily be configured on RHEL 9 using the virt-install command-line tool, the virt-manager GUI tool, or the Virtual Machines module of the Cockpit web console. This chapter will use Cockpit to install an operating system as a KVM guest on a RHEL 9 host. The chapter titled “Creating KVM Virtual Machines on RHEL 9 using virt-manager” will cover using the virt-manager tool to create new virtual machines.

The next chapter, “Creating KVM Virtual Machines with virt-install and virsh” will cover the command-line approach to virtual machine creation.

## 22.1 Installing the Cockpit Virtual Machines Module

The virtual machines module may not be included in a standard Cockpit installation by default. Assuming that Cockpit is installed and configured, the virtual machines module may be installed as follows:

```
# dnf install cockpit-machines
```

Once installed, the Virtual Machines option (marked A in Figure 22-1) will appear in the navigation panel the next time you log into the Cockpit interface:

![](img/be1f159c3cc937d7b264dc5b134856dc_183_0.png)

Figure 22-1

## 22.2 Creating a Virtual Machine in Cockpit

To create a virtual machine in Cockpit, click the Create VM button marked B in Figure 22-1 to display the creation dialog.

Within the dialog, enter a name for the machine and choose whether the installation media is in the form of an ISO accessible via a URL or a local filesystem path, or select the vendor and operating system type information for the guest request and choose the *Download an OS* option to have the installation image downloaded automatically during the installation process. If you intend to install RHEL as the guest using the OS download option, you must first generate an RHSM token and copy and paste it into the Offline token field of the VM creation screen. You can obtain a token by opening the following link in a browser, logging into your Red Hat account, and selecting the token generation button:

*https://access.redhat.com/management/api*

Also, specify the size of the virtual disk drive to be used for the operating system installation and the amount of memory to be allocated to the virtual machine:

![](img/be1f159c3cc937d7b264dc5b134856dc_184_0.png)

Figure 22-2

Click on the *Create and edit* button to build the virtual machine. After the creation process is complete, details of the new VM will appear in Cockpit, as shown in Figure 22-3:

Virtual machines > demo-vm-guest

demo-vm-guest

![](img/be1f159c3cc937d7b264dc5b134856dc_185_0.png)

Figure 22-3

As described in “An Overview of Virtualization Techniques” KVM provides virtual machines with several options in terms of network configuration. To view and change the network settings of a virtual machine, scroll down to the Network interfaces section of the VM Overview screen and click the Edit button:

![](img/be1f159c3cc937d7b264dc5b134856dc_185_1.png)

Figure 22-4

In the resulting dialog, the Network Type menu may be used to change the type of network connection, for example, from Virtual network (NAT) to direct attachment (MacVTap) or Bridge to LAN.

## 22.3 Starting the Installation

To start the new virtual machine and install the guest operating system from the designated installation media, click the Install button at the top of the overview page. Cockpit will start the virtual machine and scroll down to the Console view where the guest OS screen will appear:

![](img/be1f159c3cc937d7b264dc5b134856dc_186_0.png)

Figure 22-5

If the installation fails, check the message to see if an error occurred when opening the installation image. This usually occurs because the QEMU emulator runs as a user named qemu, which does not have access to the directory in which the ISO installation image is located. To resolve this issue, open a terminal window (or connect with SSH if the system is remote), change directory to the location of the ISO image file, and add the qemu user to the access control list (ACL) of the parent directory as follows:

```
# cd /path/to/iso/directory
# setfacl --modify u:qemu:x ..
```

After making this change, check the setting as follows:

```
# getfacl ..
# file: ..
# owner: demo
# group: demo
user::rwx
user:qemu:--x
group::---
```

mask::--x
other:::---

Once these changes have been made, click the Install button again to complete the installation.

To complete the installation, interact with the screen in the Consoles view just as you would if you were installing the operating system on physical hardware. If the console is too small to accommodate the entire guest operating system screen, click the Expand button in the top right-hand corner.

It is also possible to connect with and display the graphical console for the VM from outside the Cockpit browser session using the virt-viewer tool. To install virt-viewer on a RHEL 9 system, run the following command:

```
# dnf install virt-viewer
```

The virt-viewer tool is also available for Windows systems and can be downloaded from the following URL:

```
https://virt-manager.org/download/
```

To connect with a virtual machine running on the local host, run virt-viewer and select the virtual machine to which you wish to connect from the resulting dialog:

![](img/be1f159c3cc937d7b264dc5b134856dc_187_0.png)

Figure 22-6

The above command will list system-based virtual machines. To list and access session-based guests, launch virt-viewer as follows:

```
$ virt-viewer --connect qemu:///session
```

Alternatively, it is also possible to specify the virtual machine name and bypass the selection dialog entirely, for example:

```
# virt-viewer demo-vm-guest
```

To connect a virt-viewer instance to a virtual machine running on a remote host using SSH, the following command can be used:

```
$ virt-viewer --connect qemu+ssh://<user>@<host>/system <guest name>
```
