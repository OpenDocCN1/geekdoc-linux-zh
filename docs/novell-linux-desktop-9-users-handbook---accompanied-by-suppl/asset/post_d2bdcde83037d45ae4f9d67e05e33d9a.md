
# Access Recent Files

![](img/6e85ebc4ce06a64c82109523b60183ba_152_0.png)

# Drag File to New Location

To move a file, open the source folder and the destination folder on the desktop. Drag the file (or selected files) to the destination folder.

TIP

If you don't like dragging files from folder to folder, select Edit, Cut from the menu and then paste the file or files into the destination folder.

# Access Recent Files

You can quickly access your recently opened files from the System menu. This allows you to quickly get back to work on your most recent documents and other files.

- BEFORE YOU BEGIN
- Browse and Open Files
- Find Files

# CHAPTER 6: Managing Files

![](img/6e85ebc4ce06a64c82109523b60183ba_153_0.png)

51 Access Recent Files

## 1 Open Recently Used File List

From the NLD desktop, select System, Recent Files. A list of recently used files appears.

## 2 Select File to Open

Select the file that you want to open from the list. The file opens in its parent application.

52 Access and Save Files to a USB Memory Stick

You can access files from portable media such as USB memory stick drives. When the drive is attached to your computer, it acts the same as any other drive, and you can save, copy, move, and delete files on the drive.

When the drive is attached to the system, it is mounted by the system, so you can find it anytime that you need it in the /media folder in the file system.

- ✓ BEFORE YOU BEGIN
14 About File Commands
15 Use File Commands
16 Use Nautilus to Manage Folders
47 Browse and Open Files
48 Find Files
49 Delete Files

# Access and Save Files to a USB Memory Stick

![](img/6e85ebc4ce06a64c82109523b60183ba_154_0.png)

# Access and Save Files to a USB Memory Stick

## Insert USB Drive

Insert the USB drive into a USB port on your computer. A hardware detection dialog opens. If you want this dialog box to open each time you insert the USB drive, clear the Do Not Ask Again check box.

TIP

To remove the USB drive, make sure that you close all applications and applets accessing the drive. You can then remove the drive. If this makes you queasy, open a terminal window, type su, and then press Enter. Type the root password (and press Enter). Type mount /media/usb* and press Enter. You can type exit and then press Enter to go as root, and then type exit and press Enter again to close the terminal. In some cases, the light on the USB drive will still be blinking, but you can now remove it. If you still don't want to just yank out the drive, power down the system and then remove the USB drive.

# Close Hardware Detection Dialog

Select Yes on the Hardware Detection dialog box to open the USB drive.

139

# CHAPTER 6: Managing Files

## 3 Browse Files on USB

The USB drive window opens. You can browse the files and folders on the USB drive as needed. You can open another File Manager window if you want to copy or move files from the USB drive.

## 4 Close USB Drive Window

After you have finished working with the files and folders on the USB drive, select the Close button to close the window.

TIP

If you close the USB drive's Nautilus window, you can reopen it at any time. Open the Computer window (double-click on the Computer icon on the desktop) and then open the Filesystem. Open the /media folder, and the USB drive appears as an icon. Double-click the icon to open the drive.

## 53 Burn Files on a CD or DVD

You can burn folders and files to a CD or DVD (depending on the drive types installed on your computer) using the K3b burning software. You can create data CDs (or DVDs), create music CDs, or copy a CD. Now here's the bad news: Linux systems are up to protect direct access to devices other than the root account. So, you can log on as root, burn your CDs or DVDs, and then log off; no questions asked.

If you want to configure your system so that a "regular" user can access the burn drives and configure K3b so that it works correctly (and its core executables such as لديك have proper access), you are talking about several tweaks and changes to file attributes and configuration files.

Commands as chown and chmod are involved, and you have to do a fair amount of work at the command line as the root user to get things working properly. Going through all the possibilities is certainly beyond the scope of this book, and applying the "fixes" incorrectly can have dire consequences for your system. If you really have NLD administration in mind, you might want to consult NLD and Linux administration books such as Emmett Delaney's Novell Linux Desktop 9 Administrator's Handbook (as well as some of his other publications).

# 53 Burn Files on a CD or DVD

BEFORE YOU BEGIN

14 About File Commands
15 Use File Commands
46 Use Nautilus to Manage Folders
47 Browse and Open Files
48 Find Files
49 Delete Files

## Open K3b

From the desktop, select Programs, Multimedia, Burner. The K3b window opens. A tip window opens. Select Close to close tip.

NOTE

When you insert a burnable CD the hardware det-tion window opens. Select Yes to start tip.

## Start a Project

To start a new project, select Data Project in the menu.

NOTE

All the project types available in K3b are similar to the select Data Project.

To select the speed for the burn, select the Speed drop-down list and select a burn speed. You also have options that can be set: On the Fly allows you to burn the data directly to the CD without a copy made on the hard drive. The Only Create Image option burns an ISO image to your hard drive, which can be used to create a CD at a later time.

You may also want to enter descriptive information for the newly created CD including the volume name. Select the Volume tab of the project's dialog box. Enter a volume in the Volume Name box.

141

# CHAPTER 6: Managing Files

![](img/6e85ebc4ce06a64c82109523b60183ba_157_0.png)

## Start a Project

## Open K3b

## Select Folders and Files

## Set Burn Parameters

## Burn CD

## Open the Burning Dialog

## Burn Files on a CD or DVD

## Select Folders and Files

Use the left pane to locate the folders or files. Select a folder in the left pane to view its contents in the right pane. After you have located a folder or file, drag the item to the lower panel. Repeat the process as needed until you have added all the items to the lower panel that you want to burn onto the CD (or DVD).

158

NOTE

A space counter in the lower panel tells you the amount of space still available on the CD as you drag items onto it.

## Open the Burning Dialog

To opening the Burning dialog box (the place where you set burn parameters), select the Burn button in the lower right of K3b window.

## Set Burn Parameters

On the Writing tab of the Data Project dialog box, make sure that the correct burning device is selected (if you have multiple burners). You can also choose the writing mode, which is by default to Auto. Select the Writing Mode drop-down list and select DAO (at once), TAO (at once), or RAW (raw data).

Burning CDs and DVDs can sometimes be more of an art than a science. You may want to simulate the burn process to test your settings (select the Simulate option on the Writing tab). In some cases, you may also have to burn through a couple of CDs or DVDs to determine the best settings for your particular burning device (fortunately, CDs are relatively cheap and CD-RWs can be erased). After you establish the settings that work best for you, save them by selecting Save User Defaults.
