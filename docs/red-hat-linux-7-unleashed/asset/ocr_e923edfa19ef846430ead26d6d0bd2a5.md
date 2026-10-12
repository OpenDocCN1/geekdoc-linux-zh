# LILO and Other Boot Managers

CHAPTER 3

65

# **FIGURE 3.1**
PowerQuest’s BootMagic boot-loader features a graphical installation and setup.

![](bbox=[0.19, 0.09, 0.68, 0.3])

Click the Next button to install the BootMagic bootloader while running Windows.

# **Keep a Bootdisk Handy!**

Always create a bootdisk for Linux if asked during your Linux install! Having a boot disk can save lots of grief if things go awwry during installation or configuration of alternative bootloaders. BootMagic will write over the MBR of your main bootable hard drive, and will wipe out any previous LILO installation! if you want to use BootMagic and LILO, make sure to install LILO into the root native Linux partition first!

Follow through the next seven dialogs, filling out your user information, directory locations, and so on. You’ll then be asked if you want to create a bootable BootMagic diskette. This is a good idea, and the diskette can come in handy later on if you have trouble booting either Windows or Linux on your computer. After creating the diskette, you’ll see a BootMagic configuration dialog used to add other bootable partitions to BootMagic’s initial boot menu. Click the Add button to begin.

In order to show your Linux partition(s), click the Advanced box and then click the root Linux partition. When finished, click OK to add Linux to BootMagic’s boot menu. You’ll then be asked (in a new dialog) to give your Linux partition a name and icon. Click OK when finished, and you’ll see BootMagic’s main dialog (as shown in Figure 3.2).

The main dialog is used to set the default operating system to boot. Click your new Linux entry, and then click the Up arrow Reorder button to move Linux to the top of the list. Click the Set as Default button while your Linux entry is highlighted to make sure your computer boots to Linux by default. Note that you can set a startup delay, delete or rename entries, and enable or disable BootMagic. When finished, click the Save/Exit button and BootMagic will be installed.