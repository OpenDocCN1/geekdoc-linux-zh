![](bbox=[0.15, 0.2, 0.24, 0.27])

> You will need to have at least some space available in order to create a slice for FreeBSD. This means that you must have some space available marked Unused. This space can then be assigned to FreeBSD.

![](bbox=[0.18, 0.37, 0.26, 0.46])

> Note that if you select the A option for Use entire disk, it will erase any existing partitions on your disk, including Windows partitions. Also note that if you delete the Windows partition from within this program, your Windows installation will be completely overwritten once the installation of FreeBSD starts.

Once you have finished creating the partition for FreeBSD, press q to quit the program and move onto the next stage of the installation.

# Boot Manager

You will then be given a screen that asks if you want to install the boot manager. Unless you already have another boot manager installed such as Linux's LILO, you will want to install the boot manager here. This will allow you to boot FreeBSD, as well as to boot Windows if you currently have that installed on your system and still want to be able to use it after FreeBSD is installed.

# Creating BSD Partitions

Next, you will be given a message informing you that you need to create BSD partitions inside the fdisk partitions you created earlier. Press Enter here to get to the BSD partition table editor as shown in Figure 2.4.

Because this is the first time you have installed FreeBSD, I suggest that you choose the A option to select the auto defaults. After you have done so, your screen should look similar to Figure 2.5.

It's not important that you understand what all of these numbers mean right now. They will be explained later in the hour on hard disks and backup systems.

After you have finished editing the partitions, press q to exit the partition editor.