
TIP: Double-check that you have a boot disk for the machine, as well as a rescue disk, just in case something goes wrong when you are trying to bring it back up. See the sections “Making A Custom Boot Disk” and “Making A Rescue Disk” later in this chapter.

- 6. Shut down the machine. See the section “Shutting Down And Rebooting” later in this chapter for assistance.
- 7. Remove the media from the machine.
- 8. Turn on the machine and boot it.

## Seeing What Is Currently Mounted

Use the df command with no flags to get a list of what devices are mounted—temporarily or permanently—onto the file system. This is also a good method of quickly seeing how much of these file systems are already in use and how much room there is left.

## Navigating The File System In GNOME

GNU Midnight Commander is a fully functional desktop navigation tool provided with the GNU Network Object Model Environment (GNOME) desktop environment. Because there are many different things you can do with this tool, its use is broken down into categories.

### Opening GNU Midnight Commander At The Command Line

To open the GNU Midnight Commander when you are working in command line mode, do the following:

- 1. Enter the GUI by typing either “startx” from any account or “init 5” from root.
- 2. Log into GNOME with the account you want to navigate within.

NOTE: If your session is set to start K Desktop Environment (KDE) and not GNOME, then you will need to either go to the KDE navigation section or change which desktop environment you are using.

- 3. Close the Help browser, but leave the GNU Midnight Commander open. An example of what this window might look like is shown in Figure 3.3.

Related solution: Changing Desktop Environments Found on page: 167

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_119_0.png)

Figure 3.3 The GNU Midnight Commander for the “dee” user account.

### Opening GNU Midnight Commander Within A GNOME Session

If you are already in the GNOME GUI, do the following to open GNU Midnight Commander:

- 1. Click on the footprint icon to open the GNOME menu.
- 2. Click on the File Manager menu option. The GNU Midnight Commander opens as shown in Figure 3.3.

### Navigating Directories In GNU Midnight Commander

GNU Midnight Commander functions much as other file managers you might be familiar with. Navigation is primarily done on the left side of the screen. Each of the folders listed there refers to a directory. To navigate, use one or a combination of the following actions:

- A plus sign (+) next to a folder on the left means that you can open it and see what is inside. Click on the plus to see what subfolders there might be.
- Click on a folder on the left to see its actual contents, which show on the right.
- A minus sign (-) next to a folder on the left means that you have it expanded. If you want to close that folder, click on the minus sign.

### Browsing And Opening Files In GNU Midnight Commander

As stated before, GNU Midnight Commander functions much as other file managers you might be familiar with. File browsing and opening is primarily done on the right side of the screen. To browse and open files, do the following:

- 1. Open GNU Midnight Commander and navigate to the directory whose files you want to view.
- 2. Choose which style you want to use to browse. The styles available are shown in Figure 3.4.

The options, from left to right, are:

- **The *Icons* style**—This is chosen by clicking on the Icons button shown in Figure 3.4. When you select this form of browsing, all files are represented by icons related to their file type and directories are shown as folders, as displayed in Figure 3.5.
- **The *Brief* style**—This is chosen by clicking on the Brief button shown in Figure 3.4. When you select this form of browsing, directories have folder icons beside their names and files are listed by file name, as displayed in Figure 3.6.
- **The *Detailed* style**—This is chosen by clicking on the Detailed button shown in Figure 3.4. When you select this form of browsing, directories have folder icons beside their names and files are listed by file name. The size of the item and the last time it was modified are also included. This format is shown in Figure 3.7.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_120_0.png)

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_120_1.png)

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_121_0.png)

Figure 3.6 GNU Midnight Commander’s Brief style, showing the /opt/staroffice directory.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_121_1.png)

Figure 3.7 GNU Midnight Commander’s Detailed style, showing the /opt/staroffice directory.

- The Custom style—This is chosen by clicking on the Custom button shown in Figure 3.4. This style can be modified at your leisure. By default, this option shows directories with folder icons beside their names and files listed by file name. The item’s size and permissions are also included, as shown in Figure 3.8.

- 3. Double-click on a file or directory to open it. If Midnight Commander is not sure of what program to use to open the file, it will give you the gmc dialog box shown in Figure 3.9.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_122_0.png)

Figure 3.8 GNU Midnight Commander's Custom style, showing the /opt/staroffice directory.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_122_1.png)

Figure 3.9 GNU Midnight Commander's gmc display program dialog box.

- 4. Click on the program you want to use out of the Applications listing, or click on the Browse button to select the program by navigating through the file system.

- 5. Click on the OK button once you have selected the program to utilize. The program then opens to the file you wanted to work with.

## Navigating The File System In KDE

KDE File Manager (KFM) is a fully functional desktop navigation tool provided with the KDE desktop environment. Because there are many different things you can do with this tool, its use is broken down into categories.

### Opening KFM At The Command Line

To open the KDE File Manager from the command line, do the following:

- 1. Enter the GUI by typing either “startx” from any account or “init 5” from root.
- 2. Log into KDE with the account you want to navigate within.

NOTE: If your session is set to start GNOME and not KDE, you will need to either go to the GNOME navigation section or change which desktop environment you are using.

- 3. Click on the Personal Directories icon shown in Figure 3.10. This action opens the KDE File Manager, as shown in Figure 3.11.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_123_0.png)

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_123_1.png)

## Browsing In KFM

The KFM is simple to browse and works much like a Web browser. To move through the directory structure, do one of the following:

- Click on the item you want to open, whether it is a folder (directory) or an icon referring to a file.
- Utilize the Location text box and type “file:path” for where you want to go. For example, “file:/usr/sbin”.
- Click on the up arrow to move up in the directory tree.

TIP: Click on the Home icon to return quickly to your home directory.

## Setting Up Disk Quotas

There are two different stages to setting up usage quotas. In the first stage, you configure the machine itself to look for the quotas. In the second stage, you assign the quotas.

## Preparing The Machine

To set up your machine to look for quota information, do the following:

- 1. Log in as root.
- 2. Use the **ed** command to go to the base directory for the partition you want to enforce quotas over. You must create quotas on a partition-by-partition basis; you cannot apply them only to particular directories.
- 3. Use the **touch** command to create the files “quota.user” and “quota.group”.
- 4. Open the file /etc/fstab to edit. If you are unused to working with this file or with your favorite editor, be sure to make a backup of it first.
- 5. Locate the line that defines the partition to which you want to add quotas.
- 6. Move the cursor to the mount options column (column 4).
- 7. If you’re using vi, press “i” to enter Insert mode.
- 8. Add the text “usrquota” to the end of the current options to add user quotas. If you want to assign quotas by group, add the text “grpquota”. You also can add both. An example of what the resulting file might look like is:

```
/dev/hda3   /tmp  ext2  defaults,usrquota,grpquota  1  3
```

NOTE: If you are not sure if you want one of the options, go ahead and add it now.
