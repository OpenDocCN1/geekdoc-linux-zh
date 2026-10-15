Here, you can see that the CD writer (in this example, a CD writer/DVD reader) is present and is known by the system as device 0,0. The numbers represent the scsi bus/target/lun (logical unit number) of the device. You need to know this device number when you burn the CD, so write it down or remember it.

# Creating CDs and DVDs with Ubuntu's Graphical Clients

Although adequate for quick burns and use in shell scripting, the command-line technique for burning CDs and DVDs is an awkward choice for many people until they become proficient at it and learn all the arcane commands. Fortunately, Ubuntu provides several graphical clients.

# Nautilus

With Ubuntu, enhanced functionality has been included in the default file browser Nautilus. Under the Places menu item is a CD/DVD Creator selection. To use it, insert a blank CD or DVD into your CD-R/DVD-R drive. You must have two Nautilus windows open: one that shows the files you want to save to the CD, and a second one open to the CD/DVD Creator Folder (accessed in Nautilus by the Places menu, CD/DVD Creator) location. Click on the Write to Disc button as shown in Figure 7.17 to bring up the Write dialog; at the next dialog box, choose the format to which you want to write the disc. Nautilus CD/DVD Creator supports writing to a disc image file, commonly known as ISO. You can also give your new disc a label and tell Nautilus at what speed you want to write the disc. Finally, click the Write button to start the burning process—it is that simple!

![](bbox=[0.13, 0.72, 0.69, 0.915])

FIGURE 7.17 Creating a CD or DVD using the Nautilus browser is made easy with the drag-and-drop features it provides.

# Brasero

A relatively new addition to the Ubuntu default distribution is Brasero, an easy-to-use graphical CD and DVD burning application. Installed as part of the standard Live CD installation, Brasero is found under Applications, Sound and Video as Brasero Disc Burning.