By ditching the wizard-created IDE virtual disk and creating a new SCSI virtual disk, you can achieve faster read/write speeds in the virtual machine. However, it might be more difficult to install the guest operating system if there is no IDE drive; even PCs in the real world don’t deal well with computers that have only SCSI disks. This is most likely to cause trouble in DOS or a consumer edition of Windows.

Although you can move your CD-ROM drive from the virtual machine IDE controller to its SCSI controller even if your real CD-ROM drive is IDE, the virtual machine cannot boot from an emulated SCSI CD-ROM drive. A virtual machine can boot from a real SCSI CD-ROM drive, as long as that CD-ROM is configured as an IDE device in VMware.

# Floppy Drives

The VMware Configuration Wizard should have properly located and installed a floppy drive on your PC to be shared in VMware. You can verify the floppy settings by clicking the Floppy Drives tree, shown in Figure 5.23. VMware supports up to two floppy drives, one or both of which can be virtual floppy disk files. Some software is distributed on virtual floppy disks, including VMware Tools.

![](bbox=[0.26, 0.77, 0.71, 0.89])

Figure 5.23