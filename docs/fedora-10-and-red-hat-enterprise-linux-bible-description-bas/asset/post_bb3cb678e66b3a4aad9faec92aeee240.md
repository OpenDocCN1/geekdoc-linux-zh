
## Part II: Using Fedora and RHEL

You can find more information about how Xen works and what it is from the Xen Source Wiki (http://wiki.xource.com/wiki). In particular, select the Xen FAQ link (for information on what Xen is) or the HowTos link (for links to the user manual and specialty HowTos).

## Before installing Xen

Xen requires a lot of resources to run. Each operating system instance (referred to as a guest operating system) will need almost the full amount of resources it would need to run separately. Therefore, before you begin, make sure your system has at least the following:

- **RAM** — In general, your computer should have at least 256MB of RAM for each guest you want to have, please check the amount of RAM required for the type of Fedora you selected.

- **Hard Disk** — On top of what you need to install Fedora, you need the entire amount of disk space required by each operating system guest you install. Of course, these amounts can vary greatly, with minimal server installs starting at around 600MB and average desktop installs typically starting at 2GB or 3GB.

- **Paravirtualization (PAE) support** — Your computer's CPU must support the PAE extension. Many laptops will not have PAE support. To see if your computer has PAE support, type the following:

In this example, PAE is supported. If it were not supported, nothing would be returned.

- **Fully-virtualized guest support** — In order to run fully virtualized guests, you need Intel VT or AMD-V support, depending on your processor. Check your cpuinfo (as shown above) type grep vmx or svm (on Intel or AMD processors, respectively). If you see output, the program is supported.

- **GRUB boot loader** — A final requirement of the setup is that GRUB be your boot loader. When you install Xen, it will automatically add itself to your GRUB boot loader as a secondary choice of operating system kernels that you can choose to boot.

## Installing Xen

To run Xen in Fedora, you need to install and boot from a specially configured kernel. Xen kernel packages are not installed by default with Fedora, so you have to either select them at install time or add them. Here's how to install the Xen packages you need:

- **Using yum** — As root, type the following from Terminal window:

```
# yum install xen-runtime xen-libs xen-hypervisor xen-virt-manager
gome-applet-yum vnc xen-devel
```

Because Xen automatically adds an entry to your GRUB boot loader and installs it when you reboot, you should be ready to start Fedora with the Xen kernel. The next step is to reboot your computer. After rebooting, run the Services Configuration application from the System -> Services menu you choose. Verify that all services starting with xen are running.

## Installing a guest operating system

With Fedora up and running with the Xen kernel, the next step is to install a guest operating system to run in Xen. You can do this if you prefer to create a Xen guest with a command-line utility, try `xenguest-install.`.

For demonstration purposes, the procedure below shows how to install Fedora 7 as a virtual guest operating system on Fedora 10. Before you start, you need a network connection and the location of an online Fedora 7 repository. That location can be a local DVD that is shared via NFS connection. This procedure gives you an idea of how the feature work, before you try installing other operating systems.

- 1 Start libvirtd — If it's not already running, start the libvirt service:

```
# service libvirtd start
```

- 2 Select xenguest-install — As root user from a Terminal window, type the following:

```
# /usr/sbin/virt-manager
```

- 3 Select Xen host — Select Local host and click File -> Open Connection.

- 4 Create new guest — Right-click on local host and click New. When the new virtual system pop-up appears, click Forward. You are asked to name your virtual system.

- 5 Virtual machine — Type a name to represent this virtual machine and click Forward. Keep the name simple (one word, fairly short, and no special characters) because the name is used to represent the virtual machine in file names and menus. You are asked the location of the media.

- 6 Virtualization method — Select Paravirtualization (for faster, lightweight virtualization) or Fully Virtualized (slower, but supports more operating systems) and click Forward.

- 7 Installation Method — Type the location of an online software repository (you can also enter a kickstart file, if you have one). To use Fedora DVD instead of an online repository, you export it as an NFS share (see the following Note). Here's an example of a software repository for Fedora 7 so you can create a Fedora 7 system to run on your Fedora 10 system:

```
http://download.fedora.redhat.com/pub/fedora/linux/releases/7/Fedora/i386/os
```

NOTE: Here's how to use your Fedora DVD as a Xen guest repository. Install the nfs-utils package.
Insert the DVD. As it is mounted as /media/disk, add the line:

/media/disk * (ro)
to the /etc/exports file. Start nfs (/etc/init.d/nfs start). When you are prompted for a software repository, enter this address: nfs:localhost:/media/disk. If localhost doesn't work, try your computer's IP address.

- 8 **Storage location** — Choose to use a file on an existing file system or the device name of a partition to the installed system. For example, you could name the disk image /home/chris/xenimage as the file to use. I created a new partition as I was doing this process. Just make sure the location you use has enough disk space to hold the operating system you are to install. You are asked to allocate memory.

- 9 **Host network** — Choose how you would like your virtual system to connect to the host network. In most cases, select Virtual network. However, you can also select a physical device (such as Ethernet bridge or MAC address).

- 10 **Allocate Memory** — Type a number representing the number of megabytes of RAM you dedicate to this virtual machine and the amount you want to start with and click Forward. At least 256 megabytes of RAM are recommended. If you have more, should use more since it will improve performance. You can also select multiple CPUs (1 is the default).

- 11 **Finish** — When all the information has been entered, a summary of the information appears in Figure 5-6. The new virtual machine will appear on Virtual manager. Select it and click Open.

- 12 **Start installation** — A virtual console should appear, ready to install your guest Fedora 7.

- 13 **Install Guest** — Because you are installing Fedora 7 on a Fedora 10 system, you can basically follow the installation instructions in Chapter 2 of this book. By partitioning, you can instruct the installer to use the entire partition or you can create multiple partitions.

After Fedora is installed, you can open that virtual machine as you need from the Virtual Machine Manager. If you selected Ethernet bridging, and there is a DHCP server on your network, your virtual machine can be assigned its own IP address. You can use tools in Fedora to access the Internet and update and get new software as needed.

To manage your virtual machines from the command line you can use the xm command. To see which virtual machines are currently available, type the following:

```
# xm list
Name ID VCPUs State Time
Domain-0 0 453 1 r----- 1675.5
Fedora 264 1 243.9
```

If you want to save a snapshot of your virtual machine, use the xm command to save it to a. For example, save a virtual machine named Fedora to /tmp/virt-save, you could type the following:

```
# xm save Fedora /tmp/virt-save
```

Later, to restore the virtual machine, you could type:

```
# xm restore /tmp/virt-save
```

For details on working with Xen machines in Fedora, refer to the Fedora Xen Quickstart(http://fedoraproject.org/wiki/Docs/Fedora8VirtQuickstart).

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_290_0.png)

Figure 5-6: Virtual Machine Manager (virt-manager) lets you install and run guest operating systems.
