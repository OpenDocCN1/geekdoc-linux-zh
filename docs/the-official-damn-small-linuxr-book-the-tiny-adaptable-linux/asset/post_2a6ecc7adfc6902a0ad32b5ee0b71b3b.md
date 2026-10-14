
By answering only two simple questions, you can have your mydsl1.iso created and ready to burn. If you have a burner, you can continue the script to burn to a CD-R.

## Getting Started

Let's say that you have downloaded a nice, proven collection of extensions on your hard drive (say hda4). You know that because your extension collection is stored in a level 1 mydsl directory; these extensions all load upon boot. You have verified this by putting it all together on your target hardware platform.

Figure 11-1 shows an example of a set of MyDSL extensions being held in the mydsl directory on a hard disk partition (/mnt/hda4).

![](img/af53325d7f38f1cdafca9f44568e4ab8_233_0.png)

FIGURE 11-1 Shows a typical mydsl directory containing your extensions.

Now, you want to create a bootable CD-ROM with your collection of extensions. The CD should boot with no additional boot options and should contain the following applications:

- AbiWord—Word processor
- ALSA—Advanced Linux Sound System
- Gimp—Image-processing application
- GNU-Utils—The Busybox replacements for basic shell utilities
- GNU Cash—Cash management program
- Gnumeric—Spreadsheet
- GTK2—The GTK2 library needed by GTK2 applications
- Myplugins—A personal private extension for proprietary Firefox plug-ins

Upon boot, you want to have the Secure Shell Daemon (ssh), as well as the Filesystem in User Space (fuse) service. Your desktop should be Joe's Window Manager (jwm) and the system clock set to the US Pacific time zone. Finally, you want the Flash plug-in for Firefox to be included. You want everything to work seamlessly and provide a hands-free boot.

Sound difficult? Well, it is not. After you become familiar with the basics of DSL, from the tool options to the use of MyDSL extensions and some understanding of creating MyDSL extensions, creating a bootable CD-ROM is simple. The features just mentioned are discussed in Chapter 2, “Booting DSL,” Chapter 5, and Chapter 10, “Adding Applications and Creating Shareable Extensions.”

Here’s how….

## Booting from the DSL CD-ROM

To create a remastered DSL CD, you can work from a booted live DSL CD-ROM itself. Boot a Damn Small Linux CD, using any boot options that you would normally need to boot DSL. This process requires no specific boot options, so you would only add those required by your specific hardware. During the remastering process, you work from the booted live CD and use components on that CD to create your remastered CD.

One boot option you might want to add is the toram option. If you have enough RAM to run DSL entirely from RAM, entering toram here will let you eject the CD and insert a blank CD later in the process, so you can immediately burn your newly remastered live CD.

## Mounting a Working Directory

You most likely need to mount a Linux partition (probably from your hard disk) to hold system files, extensions, and the new image. Within that partition, you should make a directory to keep things organized. I suggest you make a directory called iso. The partition should be a Linux partition because you need to maintain Linux ownership, file, and directory permissions as you create the remastered CD.

You should only use the ramdisk (for example, /home/dsl/iso) to store your extensions, data, and other items if you are only making small additions and have plenty of RAM available. That’s because any remastering process will consume a lot of space. As was stated earlier, some users create DVD-sized images. So, assuming you have space available on a hard disk partition, use the mount tool (lower-right corner of the screen) to mount a disk partition (such as hda4) to hold your remastering software.

You do not need to mount the drive containing your extensions. However, you can use the same drive that stores your extensions. But, again, I suggest that you make a separate directory. So, for example, to create an iso directory on the hda4 partition, first mount that partition, then type the following from a terminal window (as root user):

```
# mkdir /mnt/hda4/iso
```
