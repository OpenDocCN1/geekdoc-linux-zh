
sequentially numbered. When looking at Microsoft’s file systems documentation, they list the FAT32 file system to be able to hold files with a maximum capacity of 4 GB. With VMware Workstation you are required to split your virtual disk up into 2 GB files on both traditional FAT and FAT32.

Tip: I always split my disk files up because it makes them more flexible to zip in pieces; this is advantageous if I ever have to write them onto CDs or DVDs. Also, if you need to copy a large virtual disk from one computer it is easier to do that when copying smaller chunks. It gives you the flexibility to restart a failed copy or move cycle.

11. Do not click on Next too fast on the screen where you specify your virtual disk name. I would like to draw your attention to the Advanced button. This is explained in the next step.

![](img/25fe75b93b97a021effaba85db112a52_42_0.png)

Figure 2.10: Do not miss the Advanced button.

Typically, the name that you enter here does not have a path. This means that the virtual disk file will be stored in the same directory where the virtual machine is located. VMware Workstation uses relative paths and always loads virtual disk files from its own directory. You could still specify another location on your hard disk to store the file. This would include the full path in this field.

12. If you click the Advanced button, you will be able to specify two additional settings. The first one is the location where the disk will be located on the IDE or SCSI channel. The second setting option is to change the disk mode.

![](img/25fe75b93b97a021effaba85db112a52_43_0.png)

Figure 2.11: These settings are from the Advanced settings screen.

You can configure your disk to be an independent disk. This means that if you create a snapshot of your virtual machine, which is explained in a later chapter, the disk will not be saved and all the actions that you perform will still go into the disk file.

The persistent disk mode writes all actions directly into the virtual hard disk file. The Nonpersistent disk mode keeps track of all the changes in separate REDO-files. When you power the virtual machine off, all your changes are discarded. You can switch between these modes later from the virtual machine Settings configuration.

The non-persistent disk mode is useful when you are working with software testing. You can start with the same unchanged environment after every restart (power-off/power-on).

> Tip: If you want to use this feature, set this disk mode after installing the operating system. By the way, working with Snapshots is the preferred method of using the same starting point over and over again.

You have now created your first virtual machine. Before getting started with the installation of your operating system, I will explain some useful information about the VMware Workstation interface. While most of it is self explanatory, I want to make sure that you know the basics in order to get started. Figure 2.12 shows an overview of the main control options and access to configuration options.

![](img/25fe75b93b97a021effaba85db112a52_44_0.png)

Figure 2.12: Overview of the main virtual machine control and configuration options.

## Suspend and Resume

The Power On, Power Off, and Reset buttons are the same as with a real PC. Suspend and Resume, however, may need some clarification. You can compare this feature with the Hibernate feature of laptops. If you click Suspend, the virtual machine state will freeze. In addition, hard disk activity will be stopped and the contents of the virtual machine's memory will be saved to a file on your hard disk. This .VMSS file compares to the HIBERFIL.SYS file, which Windows creates in the root of your hard drive when you use the hibernate feature.

Suspending a virtual machine for the first time (when it has been down or has been reset), used to take a long time with previous versions of VMware; sometimes up to a few minutes. This was because the .VMSS file was created on your hard drive with the same amount of RAM that was assigned to your machine. Creating that file took a lot of time. The performance of the Suspend and Resume processes has improved dramatically with version 5. This is accomplished by creating a .vmem file as soon as the virtual machine is powered on and by not waiting for you to suspend the machine.

## 3 What's New in VMware Workstation 5

In this chapter, I will introduce the new features for VMware Workstation version 5. In the chapter 2 from this book you can read how to install this version. There are some topics that are new in this version which I have not covered in this chapter, such as isochronous USB support. Another feature that is covered in this book is the new command line interface, which is covered in section 6.2.

The topics covered in this chapter are:

- Using multiple snapshots
- Cloning virtual machines
- Teaming virtual machines
- Movie Record and Playback
- Virtual Machine Importer

### What's new in VMware Workstation version 5.5

This chapter covers the new features of VMware Workstation version 5. However, when you are reading this, there is good chance that VMware has already released version 5.5. These are the features that will be included in the new release:

- Support for multiple (two) CPUs for virtual machines
- Support for 64 bit host and guest operating systems
- Integrated conversion for virtual machines from other vendors

### 3.1 Using Virtual Machine Snapshots

There is a reason that this functionality is on top of the list of new features and it is discussed first in this chapter. It has been the most requested new feature since snapshots were first introduced. It is now possible to create snapshots at multiple points in time which will give you the capability to go back to different points in the life cycle of your virtual machine. You can even branch off at the point when the snapshot was made to create a second timeline based on that snapshot. This will give you the capability to try several scenarios based on one virtual machine while having the flexibility to go back to any saved snapshot in the snapshot-tree.

I will first discuss what snapshots are and after that I will go into the details of working with the new and previously existing features of the snapshot technology.

### 3.2 Introduction to Snapshots

While working with real PCs, you might have come across this scenario: you are at 90% completion point of your new server installation and an error message appears which prevents you from continuing with the installation. Or, a blue screen appears, or the installation just hangs up. Or, maybe you are working on a new software installation and you want to try it with several options but still use the same starting point, such as a clean Linux or Windows workstation.

Due to the fact that VMware acts just as a real PC, you can find yourself in the same situation during the installation of your guest operating system. VMware Workstation contains a snapshot feature that can help you go back to a point in time that you can preset when you install your new guest operating system, or that you may have chosen as a base for all your testing.

### 3.3 What Snapshot is

When you take a snapshot of a virtual machine, the state of the machine is saved at that particular point in time. Both the disk and the memory are ‘frozen’ at the point where you create the snapshot. The configuration of the virtual machine and the state of your BIOS are also saved.

All the operations that you perform on the virtual machine from the point of taking the snapshot will be saved in separate files on the file system.

You can check the directory where the virtual machine is stored for these files:

- `<name>-Snapshotn.vmsn`
  This file contains the configuration information about the snapshot. It is also this file which keeps track of your virtual machine configuration. The snapshot files will be numbered Snapshot1.vmsn, Snapshot2.vmsn, and so on. The online documentation points out that more than 100 snapshots are being supported. How much more than 100, it does not specify. But of course, it will be limited by hard disk space.
- `<name>-Snapshotn.vmss`
  Contains the memory dump of your virtual machine
- `<name>-nnnnnn.vmdk`
  Multiple files contain the changes to your virtual hard disk. These files are numbered 000001.vmdk, 000002.vmdk, etc.
