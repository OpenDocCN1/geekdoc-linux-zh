
## Creating KVM Virtual Machines on RHEL 9 using Cockpit

For example:

```
$ virt-viewer --connect qemu+ssh://root@192.168.1.122/system demo_vm_guest
```

When using this technique, it is important to note that you will be prompted twice for the user password before the connection is fully established.

Once the virtual machine has been created, the Cockpit interface can monitor the machine and perform tasks such as rebooting, shutting down, or deleting the guest system. An option is also included on the Disks panel to add disks to the virtual machine configuration.

### 22.4 Working with Storage Volumes and Storage Pools

When a virtual machine is created, it will usually have at least one virtual disk drive. The images that represent these virtual disk drives are stored in storage pools. A storage pool can be an existing directory on a local filesystem, a filesystem partition, a physical disk device, Logical Volume Management (LVM) volume group, or even a remote network file system (NFS).

Each storage pool is divided into one or more storage volumes. Storage volumes are typically individual image files, each representing a single virtual disk drive, but they can also take the form of physical disk partitions, entire disk drives, or LVM volume groups.

When a virtual machine was created using the previous steps, a default storage pool was created to store virtual machine images. This default storage pool occupies space on the root filesystem and can be reviewed from within the Cockpit Virtual Machine interface by selecting the Storage Pools option at the top of the panel marked C in Figure 22-1 above.

When selected, the screen shown in Figure 22-7 below will appear containing a list of storage pools currently configured on the system:

![](img/be1f159c3cc937d7b264dc5b134856dc_188_0.png)

Figure 22-7

In the above example, the default storage pool is located on the root filesystem and stores the virtual machine image in the /var/lib/libvirt/images directory. To view the storage volumes contained within the pool, select the Storage Volumes tab highlighted in Figure 22-8:

![](img/be1f159c3cc937d7b264dc5b134856dc_189_0.png)

Figure 22-8

In the case of the demo guest, the storage volume takes the form of an image file named demo-vm-guest.qcow2. In addition, the pool also includes a storage volume containing the installation ISO image. To find out which storage volume a particular virtual machine uses, return to the main Virtual Machine Cockpit screen, select the virtual machine, and scroll to the Disks panel, as shown in Figure 22-9:

![](img/be1f159c3cc937d7b264dc5b134856dc_189_1.png)

Figure 22-9

Although using the default storage pool is acceptable for testing purposes and early experimentation, it is recommended that additional pools be created for general virtualization use. To create a new storage pool, display the Storage Pools screen within Cockpit and click on the Create storage pool button to display the dialog shown in Figure 22-10:

![](img/be1f159c3cc937d7b264dc5b134856dc_190_0.png)

Figure 22-10

In the above example, a new storage pool is being created named MyPool using a file system partition mounted as /MyPool within the local filesystem (the topic of disk drives, partitions, and mount points is covered later in the chapter entitled “Adding a New Disk Drive to a RHEL 9 System”). Once created, the pool will be listed within the Cockpit storage pool screen and can contain storage volumes as new virtual machines are created.

### 22.5 Summary

This chapter has outlined using the Cockpit web-based interface to create and manage KVM-based virtual machines. The Cockpit interface has the advantage of not requiring access to a desktop environment running on the host system. An alternative option is using the virt-manager graphical tool outlined in the next chapter.

## Chapter 23

## 23. Creating KVM Virtual Machines on RHEL 9 using virt-manager

The previous chapter explored how to create KVM virtual machines on RHEL 9 using the Cockpit web tool. With the caveat that virt-manager may one day be discontinued once the Virtual Machines Cockpit extension is fully implemented, this chapter will cover using this tool to create new virtual machines.

### 23.1 Starting the Virtual Machine Manager

If you have not already done so, install the virt-manager package as follows:

```
# dnf install virt-manager
```

Next, launch Virtual Machine Manager from the command line in a terminal window by running virt-manager. Once loaded, the virtual machine manager will prompt for the password of the currently active user before displaying the following screen:

![](img/be1f159c3cc937d7b264dc5b134856dc_191_0.png)

Figure 23-1

The main screen lists the current virtual machines running on the system. By default, the manager should be connected to the system libvirtd instance. If it is not, connect to the host system by right-clicking on the entry in the list and selecting Connect from the popup menu. To manage session-based virtual machines, select the File -> Add Connection... menu option to display the dialog shown in Figure 23-2:

![](img/be1f159c3cc937d7b264dc5b134856dc_191_1.png)

Figure 23-2

Select QEMU/KVM user session from the Hypervisor menu and click the Connect button within this dialog. On returning to the main *virt-manager* screen, the QEMU/KVM session should now be listed as shown in Figure 23-1 above.

To create a virtual system, click on the new virtual machine button (the far left button in the toolbar) to display the first screen of the New VM wizard. In the Name field, enter a suitably descriptive name for the virtual system. On this screen, also select the location of the media from which the guest operating system will be installed. This can either be a CD or DVD drive, an ISO image file accessible to the local host, a network install using HTTP, FTP, NFS, or PXE, or the disk image from an existing virtual machine:

![](img/be1f159c3cc937d7b264dc5b134856dc_192_0.png)

Figure 23-3

### 23.2 Configuring the KVM Virtual System

Clicking Forward will display a screen seeking additional information about the installation process. The displayed screen and information required will depend on selections made on the initial screen. For example, if a CD, DVD, or ISO is selected, this screen will ask for the specific location of the ISO file or physical media device. This screen also attempts to identify the type and version of the guest operating system (for example, the Windows version or Linux distribution) based on the specified installation media. If it is unable to do so, uncheck the *Automatically detect from installation media/source* option, type in the first few characters of the operating system name, and select an option from the list of possible matches:

![](img/be1f159c3cc937d7b264dc5b134856dc_193_0.png)

Figure 23-4

Once these settings are complete, click the Forward button to configure CPU and memory settings. The optimal settings will depend on the number of CPUs and amount of physical memory present in the host, together with the requirements of other applications and virtual machines that will run in parallel with the new virtual machine:

![](img/be1f159c3cc937d7b264dc5b134856dc_193_1.png)

Figure 23-5

On the next screen, options are available to create an image disk of a specified size, select a pre-existing volume, or create a storage volume of a specified format (raw, vmdk, ISO, etc.). Unless you have a specific need to use a particular format (for example, you might need to use vmdk to migrate to a VMware-based virtualization environment at a later date) or need to use a dedicated disk or partition, it is generally adequate to specify a size on this screen:
