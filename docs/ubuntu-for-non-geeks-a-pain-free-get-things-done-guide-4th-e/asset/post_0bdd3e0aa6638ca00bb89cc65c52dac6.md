
Figure 15.4: Selecting Rhythmbox as the application to use when working with the audio files on your generic MP3 player

Figure 15.5: Adding songs to your digital audio player via Rhythmbox

## Copying Songs from Your Audio Device to Your Hard Disk

One feature of most digital media players that isn’t available in iTunes (at least not without the installation of a special freeware plug-in) is the ability to copy songs from your iPhone/iPod to your hard disk (or even to an external USB drive). Luckily, Rhythmbox allows you to do this quite easily.

To copy music from your iPhone/iPod, Android based phone, or other digital media device with Rhythmbox, select the tracks you want to export (hold down the CTRL key to make multiple selections, or use the tabs to select whole artists or genres if you like), and drag the selected items to your desktop, music folder, or wherever you want them. The only catch with this seemingly simple approach is that when copying files from an iPod/iPhone, you end up with files on your hard disk with funky filenames, such as ZPAD.m4a or ATDT.mp3, rather than the name that appeared on your iPhone/iPod or within Rhythmbox. This means you’ll have to rename the files once they have been transferred to your hard disk, which isn’t much of a chore unless you’re dealing with lots and lots of files or if you just forget which file is which. In case of the latter, right-click the file, click Properties, and then click the Audio tab, where you will find the original filename (Figure 15-6). Once you know it, click the Basic tab, type the correct name in the Name box, and then click Close.

![](img/f7cef0df22f9dba5a41777808c98eece_321_0.png)

Figure 15-6: Finding the file properties of a mislabeled audio file

## Ejecting Your iPod or Other Digital Device from Within Rhythmbox

When you’re done working with your iPod or other digital device in Rhythmbox, you can eject it either by clicking its entry in the left pane of the Rhythmbox window and then clicking the Eject button near the top of the window or by right-clicking its icon in the left pane and selecting Eject in the pop-up menu that appears. If Rhythmbox is closed, this right-click-to-eject approach also works from within a Nautilus window or with the desktop icon for a mounted device.

## Problems Writing to Your iPod

If you have an iPod (iPhones and iPod touch not included) that you were last using in conjunction with a Mac, you may find that although you can read the files on your iPod, you cannot write files to it. It is most likely that your iPod is formatted in Apple’s native HFS+ filesystem, although this in itself is not a problem. The problem is that HFS+ formatted iPods have journaling enabled. journaling is an HFS+ feature that acts to protect the filesystem from damage due to power surges, power failures, or hardware breakdowns.

As fate would have it, however, the Linux kernel doesn’t deal well with journaling-enabled, HFS+ formatted devices. Fortunately, the tweak to fix this is quite simple, and it isn’t even particularly geeky: You just have to disable journaling on your iPod.

Disabling journaling on an HFS+ formatted iPod is a very easy task if you have a Mac nearby. Just plug your iPod into a Mac, close iTunes when it automatically opens, and then run Disk Utility (in the Utilities folder within the Applications folder). When Disk Utility opens, select your iPod (by name) in the left pane of the window, press the OPTION key, and then choose Disable Journaling in the File menu. After a moment, journaling on your iPod will be disabled without any loss of data. If you connect your iPod to your Linux machine again, you will be able to use it more or less like normal.

## Working with Photos on Your Digital Device

As I already mentioned, if your phone or digital device is photo-capable and Ubuntu automatically recognizes it, you will be led to F-Spot Photo Manager, just as you are when you hook up your digital camera to your Ubuntu machine. In the same way, F-Spot takes stock of what you have on your device and then allows you to copy photos to your hard disk.

As you can see in Figure 15-7, you first select the photos you want to copy to your hard disk, add a tag if you like, and then click Copy. After the photos are copied to your disk, they will appear in the main F-Spot window (Figure 15-8), from which you can work with them as you see fit.
