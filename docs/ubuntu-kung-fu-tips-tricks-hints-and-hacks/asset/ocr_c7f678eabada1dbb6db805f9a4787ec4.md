So, whereas a path like `C:\Documents ... and Settings\Owner\My Documents` is common under Windows, you will see something like `/home/frank/Documents` in Ubuntu. This difference can be jarring at first, but you’ll be surprised at how quickly you get used to it.

# Mounting

If there are no drive letters then how are other storage devices accessed, such as CD/DVD drives, or USB memory sticks?

The answer is that they’re *mounted*—effectively, the filesystem of the storage device is magically plumbed through to a particular folder within the Ubuntu filesystem. Insert a CD/DVD, for example, and its contents will be visible when you browse to the `/media/cdrom` folder.

It’s important to note that the files aren’t literally copied to the folder. They’re made available in a virtual way. You can manipulate the files and folders like any other files and folders, and although it might appear as if they’re contained in that particular folder, they aren’t.

Anything that might have already been in the folder used as the *mount point* will temporarily disappear. However, the contents are still there, and if the storage device is *unmounted*, the contents will reappear.

Mounting might sound complicated, but don’t worry—it’s nearly always done automatically, either at boot-up for devices permanently attached to your PC, or when you attach a removable storage device to the computer, such as a USB stick. You probably won’t be aware of it taking place, in fact; all the user sees after inserting a USB memory stick is a new icon on the desktop that, when double-clicked, lets her browse the USB stick’s files. Of course, if the user looks closely, she will see that she’s actually browsing the folder that the USB memory stick has been mounted at.

# File & folder names

File and folder names can contain spaces, as with Windows, but upper/lowercase letters are important in Linux. A folder can feasibly contain separate files called `Report.doc`, `REPORT.doc`, `report.doc`, `REPORT.doc`, and so on.

See Figure 4-1 for an example of this in action. The top half of the screenshot shows an attempt to rename a file to `REPORT.doc` in Windows, when a file called `report.doc` already exists in that folder. This isn’t allowed because Windows is unable to tell the difference between