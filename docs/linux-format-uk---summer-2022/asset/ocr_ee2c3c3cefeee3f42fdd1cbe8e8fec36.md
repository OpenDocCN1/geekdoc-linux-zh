# ## Guide

### **CHANGING LOCATION**

### **AFTER YOU MOUNT A FILE SYSTEM**

### **WE'RE GOOD TO GO**

### **MAKING THE CONNECTION**

Guide
mount /mnt /usr/media/usb2

### **CHANGING LOCATION**

The $\Delta$ (df) mount /usr/1st /dev/hda2

The /dev/hda2 partition is the root of our /dev/hdb. After booting, it gets mounted, and the root device is /dev/hdb. A mount table (also called a file table) will show all mounted file systems. For a /dev/hdb root file system you'll see it in /etc/fstab. To mount or unmount a file system manually, use the mount and umount (or $\mathrm{um}$) commands. In order to make a new file system on the new root device, you'll need to run the $\mathrm{mkfs}$ command (for creating ext3 filesystems, you'll run the mkfs.ext3 command). In order to unmount a file system, just use the umount command. Remember, it's important to keep the mount point and the device name straight.

### **AFTER YOU MOUNT A FILE SYSTEM**

Once the file system is ready, you can add a new user (just like you would have added one with useradd, you can then set the password for the user with passwd). You can now install programs. There are two ways to install packages: 1) by using apt-get (or equivalent software installation packages on other distros), or 2) manually downloading the binary and installing it.

### **WE'RE GOOD TO GO**

Now for the important part. The whole reason to have Linux is to be able to use the computer as you like, not just as it comes out of the box. There are so many things you can do with Linux that I can't cover them all here. You can create a full desktop environment by installing a display manager and a window manager. You can install audio, video, and graphics drivers. You can even burn CDs and DVDs. The possibilities are endless. Just start installing things and you'll be surprised at what you can do.

### **MAKING THE CONNECTION**

To make sure your network is ready to go, you can run the $\mathrm{ifconfig}$ command on your system. If you've installed the network software, you'll see your network card listed (for example, eth0). You can also check your IP address with the $\mathrm{ip}$ command. To test your connection, you can use the ping command to check a host on the network. To check the status of your connection, you can use the $\mathrm{netstat}$ command. The $\mathrm{netstat}$ command displays information about your network interfaces, routing tables, and other network statistics.

![](bbox=[0.55, 0.45, 0.95, 0.75])

> > **QUICK TIP**
> > As a tip,
> > the 'df' command
> > will tell you
> > what is mounted
> > on your system.

> > **GIVE ALL YOUR DETAILS TO US!**
> > If you have any questions, feel free to email us at your address.