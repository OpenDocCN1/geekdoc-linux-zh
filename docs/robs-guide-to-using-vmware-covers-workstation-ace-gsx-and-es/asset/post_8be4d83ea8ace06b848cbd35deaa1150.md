
The only disadvantage of this procedure is that you will not see what is happening. However, from the disk and network activity on your computer or inside your virtual machine you will be able to tell that the process is sending the disk information from source to destination.

## Where to go from here

Depending on the operating system that you are restoring, you may need to modify drivers, etc. This is explained in detail in chapter 21: “Modify your restored operating system to work with VMware”.

## 20.4 Preparing your Computer for Smaller Images

When you create a hard disk image with an imaging utility such as g4u or the dd command which just reads blocks from the hard disk and stores them in a file, that file by default becomes the same size as your hard disk. Even when g4u performs compression on the file it creates, it depends on your hard disk whether the compression is efficient. Blocks on the hard disk may seem empty, but they are not. And g4u does not contain drivers for all file systems, so it is not aware of the way that your hard disk is being used. Therefore, it is a good idea to prepare your hard disk from within the operating system. You do this by filling all the blocks that are not used with bytes which contain the same value: zero.

There are tools and commands available for this for every operating system. I have listed the most common ones here:

### Unix/Linux

Use the default dd command to create the file and delete it afterwards:

```
dd if=/dev/zero of=/zerofile bs=1m
rm /zerofile
```

The first command uses the if parameter to specify the special /dev/zero device, and it sends the output to the file specified with the of parameter. The bs parameter specifies that every write cycle to the file is written in 1 MB chunks. The second command then removes the file. You must do this for every partition that you will be imaging.

### Windows

For Windows, one of the freely available tools, available under the GNU General Public License is Eraser. It is available from the following URL: sourceforge.net/projects/eraser.

### NetWare

On a NetWare server, use the FILLZERO.NLM to fill all unused blocks with zeros. The file is available from the tools section on the author's website at the following URL: www.robbastiaansen.nl.

## 21 Modify your Restored Operating System to Work with VMware

Once you have restored an image to a virtual machine, you will need to modify the operating system to load the correct drivers for the hardware that is used in VMware. This section will explain how to do that for Windows, Linux, and NetWare operating systems.

### 21.1 Windows 9x Operating Systems

Windows 95, 98 and ME are the simplest of all Windows versions to image to different hardware compared to what the source computer is running. They do not have anything such as Hardware Abstraction Layer that you need to take care of after imaging. It is my experience, that the Plug and Play capabilities of these versions of Windows find all the hardware in your virtual machine.

### 21.2 Windows NT/2000/XP/2003 Operating Systems

These versions of Windows have a so called Hardware Abstraction Layer module which is installed on a PC during installation. If you move a disk into other hardware (whether physically or when restoring to a virtual machine), you will have to manually modify this HAL.DLL to the one needed for Windows in VMware.

Furthermore, you need to add the correct drivers to your virtual machine for your video adapter, sound adapter, network adapter, etc. Also, you should keep in mind that by default the mass storage drivers are not replaced. Therefore, you need to make sure that you image from a computer with an IDE disk to a virtual machine with an IDE disk and from a computer with an SCSI disk to a virtual machine with an SCSI disk. At the end of this section I have added detailed information on how to image a Windows machine from an IDE disk to a SCSI disk.

Note: Imaging Windows PCs is something that falls outside the scope of this book. Microsoft’s official position is that you need to use the SYSPREP utility to prepare a Windows machine, and there are many items to take care of. An example of this is the Security Identifier (SID), which is especially important when a workstation is part of a domain.

The following links to SYSPREP information by Microsoft will help you get started if you want to use this utility:

```
msdn.microsoft.com/library/default.asp?url=/library/en-us/dnw2kmag00/html/sysprep.asp
```

www.microsoft.com/technet/prodtechnol/windows2000pro/deploy/depopt/sysprep.mspx

www.microsoft.com/resources/documentation/Windows/XP/al1/reskit/en-us/prbc_cai_vnve.asp

The steps that I will describe below do not require the use of SYSPREP. Be aware that it is not guaranteed that it will work in your environment.

To replace the HAL.DLL with the one you need for VMware, one of the possible methods is described here:

- 1. Find out what the HAL.DLL is; you will need it for your specific version of Windows and the installed service pack. The easiest approach is to install the same version of Windows and service pack into a virtual machine, and copy the HAL.DLL to your host PC.
- 2. When you have the correct HAL.DLL, you need to add it to the restored machine. You could have copied it to the original PC, before taking an image, but you can also add it to the newly restored disk by mounting it with the VMware DiskMount utility as explained in section 7.4: “Using the DiskMount Utility”
- 3. When you have loaded the Windows operating system, and you now have the correct Hardware Abstraction Layer, it will start detecting the hardware in your virtual machine. It is a good idea to make sure that you have the driver files available in the virtual disk file or in an ISO file which you can attach to the virtual machine.
- 4. When all the hardware is detected and all the matching drivers are found, do not forget to install the VMware tools.

Tip: It might also be convenient to add the i386 directory from the Windows installation CD-ROM or the Service Pack source files, into the virtual disk when you have it mounted with the VMware DiskMount utility. That way if files are needed, they are easily available.

### Microsoft Product Activation

When imaging Windows XP or Windows 2003, depending on the type of license being used, you may have to activate Windows again. Make sure that the machine is completely configured with all the new hardware before activating Windows.

![](img/25fe75b93b97a021effaba85db112a52_208_0.png)

Figure 21.1: After a restore Windows might need to be activated.

### Imaging from IDE to SCSI

It is possible to restore an image of a computer with an IDE device into a virtual machine with an SCSI device. An example of this is when you restore into an ESX Server virtual machine, since that server only supports SCSI virtual disks. The trick is to install the VMware SCSI driver into the machine, before creating the image. Prepare for this configuration by downloading the Windows SCSI drivers from the following URL: www.vmware.com/download. The download is a virtual floppy. You can extract it with Winimage or mount it with the Virtual Floppy Driver. This is explained in chapter 7.

You do this from the Add Hardware Wizard. You need to start the wizard from the System Properties window in the Control Panel. Perform the following steps when the wizard runs (this example is based on Windows XP):

- 1. The wizard asks you if you have already installed the hardware in the computer. Select yes here, even when there is no VMware SCSI disk present.
- 2. At the bottom of the installed hardware list, select Add a new hardware device and select Next.
- 3. In the next window, select the option to manually select the hardware that is installed.
- 4. When a list of hardware categories to install from is displayed, select the top item called Show all devices.
- 5. In the device driver selection window, click the button Have Disk.
- 6. Browse to the vm scsi .inf file and click Ok.
