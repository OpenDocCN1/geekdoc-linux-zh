# Microsoft Product Activation

When imaging Windows XP or Windows 2003, depending on the type of license being used, you may have to activate Windows again. Make sure that the machine is completely configured with all the new hardware before activating Windows.

![](bbox=[0.07, 0.24, 0.8, 0.49])

Figure 21.1: After a restore Windows might need to be activated.

# Imaging from IDE to SCSI

It is possible to restore an image of a computer with an IDE device into a virtual machine with an SCSI device. An example of this is when you restore into an ESX Server virtual machine, since that server only supports SCSI virtual disks. The trick is to install the VMware SCSI driver into the machine, before creating the image. Prepare for this configuration by downloading the Windows SCSI drivers from the following URL: www.vmware.com/download. The download is a virtual floppy. You can extract it with Winimage or mount it with the Virtual Floppy Driver. This is explained in chapter 7.

You do this from the Add Hardware Wizard. You need to start the wizard from the System Properties window in the Control Panel. Perform the following steps when the wizard runs (this example is based on Windows XP):

+   1. The wizard asks you if you have already installed the hardware in the computer. Select yes here, even when there is no VMware SCSI disk present.
+   2. At the bottom of the installed hardware list, select Add a new hardware device and select Next.
+   3. In the next window, select the option to manually select the hardware that is installed.
+   4. When a list of hardware categories to install from is displayed, select the top item called Show all devices.
+   5. In the device driver selection window, click the button Have Disk.
+   6. Browse to the vm scsi .inf file and click Ok.