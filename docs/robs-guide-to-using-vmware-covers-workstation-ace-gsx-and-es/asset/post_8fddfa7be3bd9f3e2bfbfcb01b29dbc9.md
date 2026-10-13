
Although Acronis True Image 8.0 Server for Windows takes care of hard disk and filesystem-level consistency via snapshot technology, it could not guarantee application-level consistency. We recommend you to suspend complex servers such as Microsoft SQL, Oracle or Microsoft Exchange before pressing the Proceed button on the last page of the Acronis True Image 8.0 Server for Windows Create Image wizard, or before starting a scheduled task. Once the imaging process starts, you can resume server operations. It is not necessary to suspend the applications for the duration of the imaging process.

As you can read in the previous text, it is safe to execute an imaging operation from a running Windows host. But is it wise? What will happen to the disk and network performance when all regular tasks are running and you pull an image off the server? It all depends on the load of your server, but I suggest that you create the image when no other users are working with the server or at least during off-peak hours.

Note: Running the imaging operation with no users attached, is especially important if you are migrating a server into a virtual environment permanently. Once the imaging has been completed, nothing that goes into the physical machine will ever be added to the virtual machine.

## 18.1 Creating the Image

You can start the imaging in two ways, as explained earlier. You can either start with the True Image rescue CD or install the application on your Windows or Linux host. When you install the application, you will be prompted to create the Rescue Media (see Figure 18.1). With that CD-ROM or a set of floppies, you can boot your PCs or virtual machines to create images or restore them.

Tip: To use the rescue CD-ROM inside a virtual machine, it is best to use an ISO-file. How to create an ISO file from a CD-ROM is explained in detail in chapter 7.

To create the image, start the application or boot your computer with the Rescue Media. Once you see the main application screen with the option Create Image, all the steps are identical to what follows, no matter how you get to this point.

![](img/25fe75b93b97a021effaba85db112a52_197_0.png)

The Acronis software lets you create the Rescue Media during installation or after that, when you select Tools → Create Bootable Rescue Media. It depends on the hardware you have installed what write options you have available. Using floppies requires 6 floppy disks so I really recommend using a CD-ROM instead.

Figure 18.1: Create the Bootable Rescue Media during installation or later from the application.

Creating the image is wizard based. You can go through the selection of which hard disk and which partitions you want to restore. Once you have selected your source, it is time to select the destination. You can store the image on a local hard disk but the cool thing about Acronis True Image is that you can store the image directly on a network location. With the Windows version, as well as with the Rescue Media this can be another Windows machine.

![](img/25fe75b93b97a021effaba85db112a52_197_1.png)

In the Linux version, you can also use Windows shares by selecting the Samba Network option. However, it is also possible to directly access NFS network resources. But both options and all other types of destinations will work, if you mount them to a local directory and use that as the destination.

Figure 18.2: True Image allows you to store the image on a networked destination directly.

Acronis True Image allows you the option to add a password to the image file and a description, where you can add information about the machine where the image was created from, the date, and other information that might be relevant at restore time.

## 18.2 Restoring the Image

What can I say? If you have read the previous section on how to create the image, then there is not much more to say about restoring the image. You can also boot with the Rescue Media and browse the network to select the source image file. Then you can select the destination hard disk and partition and restore the image to the machine.

![](img/25fe75b93b97a021effaba85db112a52_198_0.png)

There is one tip that I would like to give you when restoring images. Make sure the destination drive is large enough to contain the source partition. If it is too small, the Restore Image Wizard will not show that disk as a destination for your restore. This should of course never be a problem with restoring inside a virtual machine where adding a large enough hard disk is just a matter of a few mouse clicks.

Figure 18.3: Select a destination that is large enough to contain the image to be restored.

## Where to go from here

Depending on the operating system that you are restoring, you may need to modify drivers, etc. This is explained in detail in chapter 21: “Modify your restored operating system to work with VMware”.

## 19 Create a Virtual Disk from an Image File (for any imaging application)

With the imaging operations described in the previous parts for peer-to-peer imaging and imaging to network destinations, you rely on a network connection being available. In addition, you rely on network drivers that are operating correctly. This is not always the case, and therefore, I also describe another approach where only disks are involved. Therefore, this procedure is supported by all operating systems and with all imaging applications.

To restore an image of a physical machine into a virtual machine, with this method, you need to first create an image file by using the method which works best for you (with your favorite imaging application). Then you need to create a virtual machine, and restore the image inside the virtual machine. Of course, you still have to edit your restored operating system to work with the virtual machine hardware as described in chapter 21: “Modify your restored operating system to work with VMware”.

The short description of the method that is described here is that we create a virtual machine with two disks. One will hold the image file, and the other will be the destination disk. You then boot with your boot-medium from your imaging solution and restore the local disk file.

- 1. At this point I am assuming that you have already created the image file with the imaging application of your choice.
- 2. Create a virtual machine with the settings that reflect your destination operating system (Windows, NetWare, etc.). Create a disk that is the same type as your original disk from the physical PC (IDE or SCSI), and make it large enough to receive the restored image file.
- 3. Next, you will need to add a disk that will hold the image file. There are two approaches to this; first I will discuss the one for the gui-users:
  - Use a Windows or Linux virtual machine with a second disk to format the disk, and copy the image file into that separate virtual disk via either the network or by a Host-to-Guest shared folder.
  - Next, I will discuss the one for those who are into the command line stuff:
  - Create a virtual disk with a FAT file system (or download an empty disk Empty1999mbFATdiskv4.zip or Empty1999mbFATdiskv5.zip from the tools section at www.robbastiaansen.nl).
  - Mount the empty disk with the DiskMount utility (described in section 7.4: “Using the DiskMount Utility”).
  - Copy the image file into the virtual disk.
  - Dismount the disk file and attach it to the virtual machine, where you will be restoring the image.

```
vmware-mount k: Empty1999mbFATdisk.vmdk
```

- 4. At this point, you have a virtual machine with an empty disk (disk 1) and a disk containing the image file.

- 5. Start your virtual machine now, with the boot media from your imaging solution. This can be a (virtual) boot floppy or CD-ROM created for Ghost, DriveImage, or any other solution. In addition, if you own ZENworks for Desktops, you can use the CD-ROM iso file to boot the virtual machine.

![](img/25fe75b93b97a021effaba85db112a52_200_0.png)

Tip: If you are using Ghost, then you can find the procedures for creating a virtual boot floppy in section 16.1: “Creating the Ghost boot disk for VMware”

![](img/25fe75b93b97a021effaba85db112a52_200_1.png)

Tip: If you use Novell ZENworks imaging with the bootcd.iso which comes with ZENworks for desktops, you should mount the second disk in the system (that holds the image file) with the following command: mount -t msdos /dev/hdb1 /mnt/harddisk. You should then restore the local image with the following command: img rl /mnt/harddisk/<imagefile.zmg>.

```
mount -t msdos /dev/hdb1 /mnt/harddisk
```

```
img rl /mnt/harddisk/<imagefile.zmg>
```

- 6. You can now restore the local image file with your imaging solution. Depending on the operating system that you are restoring, you may need to modify drivers, etc. This is explained in detail in chapter 21: “Modify your restored operating system to work with VMware”.
