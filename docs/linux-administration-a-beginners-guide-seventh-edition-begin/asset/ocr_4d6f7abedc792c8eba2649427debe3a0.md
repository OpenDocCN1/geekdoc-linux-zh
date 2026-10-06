# 792 Linux Administration: A Beginner's Guide

| Option | Description | Value(s) |
| --- | --- | --- |
| --name | Name of virtual machine/ guest instance. | abg-7e-vm |
| --ram | RAM (memory) to allocate to VM guest, in MiB. | 2000 |
| --disk | Specifies the path to the VM image that you are importing, as well as other storage-related options. | /home/vms/abg-7e-vm -qcow2,bus=virtio,format=qcow2
Specifies the path to the VM image file, a bus option of virtio, and format option of qcow2). |
| bus | Virtual disk type | |
| --format | Disk image format | vnc,listen=0.0.0.0,port=5910,password=abg |
| --graphics | Specifies the graphical display configuration. | (These options will set up a VNC server listening on port 5910 on the host system. The password to connect is abg.) |

+   * --noreboot | Prevents the demand from automatically rebooting after the install or import completed.

+   * --import | Skips the OS installation process, and imports a guest from an existing image.

# Table B-1 virt-install Options

2. Use the virt-install utility to import the VM image. The virt-install utility supports several options that allow you to customize the new VM. The requirements/parameters that use are described in Table B-1. Import the VM by running

```
[root@host vms] # virt-install \ \
--name abg-7e-vm \ \
--memory 2000 \ \
--disk /home/vms/abg-7e-vm.qcow2,bus=virtio,format=qcow2 \ \
--graphics vnc,listen=0.0.0.0,port=5910,password=abg \ \
--noreboot \ \
--import
```

# Managing the Demo Virtual Machine

In the preceding section, we walked through the process of importing and creating a new virtual machine from an existing image. In this section, we will look at some typical tasks associated with managing guest virtual machines.