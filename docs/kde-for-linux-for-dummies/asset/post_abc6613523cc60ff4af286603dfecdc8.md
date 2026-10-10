
Figure 4-9:
The KFM Configuration dialog box contains some important settings.

![](img/8dd43d91b80664e771e0c0a824d7392d_97_0.png)

When you get KFM configured the way you like it, choose Options Save Settings to make the current KFM configuration the default. New KFM windows will then appear with the same view and other configuration settings as the current KFM window, instead of the original installation defaults.

## Creating a New Folder

Creating new document files is something that you probably do in your various application programs. But creating the folders in which to store those documents is a job for KFM. To create a new folder, follow these steps:

1. Open KFM and navigate to the location where you want to create the new folder.

You can use any of the techniques mentioned elsewhere in this chapter to open a KFM window and to navigate to the directory in which you want to create the new subfolder.

![](img/8dd43d91b80664e771e0c0a824d7392d_97_1.png)

In order to create a new folder, you must have appropriate access permissions for the directory where you are creating it. If you are logged on under a regular user name, you are generally restricted to creating new folders in your home directory and its subdirectories. If you are logged on as the superuser, root, then you can create folders anywhere in the file system.

2. Choose File New Folder or right-click the KFM window and choose New Folder from the pop-up window that appears.

KFM opens the dialog box shown in Figure 4-10, prompting you for the name of your new folder.

![](img/8dd43d91b80664e771e0c0a824d7392d_98_0.png)

3. **Type a name for the new folder** and then click the **OK** button.

KFM closes the dialog box and creates the new folder. The folder name and icon appear in the KFM window.

After you create a new folder, you can copy and move files into it (see the “Copying and Moving Files” section of this chapter) and use the folder as the location in which you create new document files.

![](img/8dd43d91b80664e771e0c0a824d7392d_98_1.png)

When you create a new folder, it starts out with the access permissions set to allow you, the owner, full access and to prevent all other users (except the superuser) from accessing the directory. If you want to allow others to access your new folder, you must change its permission settings. To do that, follow these steps.

1. **Right-click** the folder name or icon in the KFM window and choose **Properties** from the pop-up menu that appears.

KFM opens a dialog box where you can edit the properties of the selected folder. (You can use the same technique to edit the properties — including access permissions — for files as well as folders.)

2. Click the **Permissions** tab.

KFM displays the options shown in Figure 4-11.

![](img/8dd43d91b80664e771e0c0a824d7392d_98_2.png)

3. Click checkboxes in the **Access Permissions** area to select or deselect access permissions as needed.

- The default settings shown in Figure 4-11 allow full access by the owner (you) but deny access to others. Add checkmarks to other boxes to grant various forms of access to other groups of users.

- If you're logged on as a regular user, you can't change the ownership of a file or folder. So the Owner and Group settings are grayed out. To change those settings, you must be logged on as the superuser.

4. **After adjusting the permission settings, click the OK button**.

KFM closes the dialog box and changes the access permission settings for your folder.

Refer to Chapter 13 for more information on access permissions and on using KFM in superuser mode to perform file management tasks that you can't do as a normal user.

## Copying and Moving Files

Perhaps the most common file maintenance task you'll do with KFM is to copy or move a file from one directory to another. KFM makes it easy to do. Whether you're moving or copying a file, the basic procedure is the same — and it's a simple drag-and-drop operation between two KFM windows. The following steps outline the procedure in detail:

1. **Open a KFM window and navigate to the directory containing the file you want to copy or move.**

- If necessary, scroll the KFM window so the file you want to move is readily accessible.

2. **Open a second KFM window and navigate to the destination directory.**

- Make sure the KFM window displays the directory into which you want to copy or move files. Position the window on your desktop so it will not be obscured by the other KFM window.

- A quick way to open another KFM window is to click the gear icon at the right in the KFM toolbar. A new window appears displaying the contents of the same directory.

- Normally, you copy or move files from one directory to another — hence the two KFM windows. However, you can also copy and move files directly to the KDE desktop. In that case, the second KFM window is not necessary.

3. **Click the first KFM window's titlebar.**

- This brings the source KFM window to the foreground — gives it the focus.

4. Click and drag the file from the source KFM window to the destination window. Release the mouse button to drop the file on the destination window.

A small pop-up menu appears giving you the option to Copy, Move, or Link.

5. To copy the file, choose Copy. To move it, choose Move.

Copying a file makes an exact copy of the file in the new directory and leaves the original file in its original location. Moving a file makes a copy of the file in the new directory and removes the file from the original location.

![](img/8dd43d91b80664e771e0c0a824d7392d_100_0.png)

![](img/8dd43d91b80664e771e0c0a824d7392d_100_1.png)

The third option (Link) on the pop-up menu that appears when you drag-and-drop a file from a KFM window creates a symbolic link file in the destination directory that points to the original file in the source directory. (Creating a Link is roughly equivalent to creating a shortcut icon in Windows.) Sometimes creating a symbolic link is preferable to creating a copy of a file. A link creates the appearance of having a copy of the file in the new location, but the link is usually much smaller than the original file and, because clicking the link actually opens the original file, there’s no problem with two copies of the same information getting “out of sync.” If you’re not familiar with symbolic links, refer to a general Linux or UNIX book.

## Deleting Files

Another common file maintenance chore is getting rid of outdated and otherwise unwanted files and folders. KDE provides two options for disposing of unwanted files. The KDE trash can enables you to remove files in such a way that you can later recover them if necessary. You can also remove files from your system permanently and completely with KFM’s Delete command.

### Trashing files

![](img/8dd43d91b80664e771e0c0a824d7392d_100_2.png)

The KDE Trash appears on your desktop as a cute little trash can icon. However, the Trash is really a special-purpose folder (~Desktop/Trash/) that serves as the temporary storage space for files and folders on their way to being removed from your system.

Placing a file or folder in the Trash folder is analogous to dropping papers into your office trash can. Files that are in the Trash are out of sight and out of mind, but they aren't yet out of your office. If you discover that you made a mistake and trashed the wrong file, you can dig into the trash can and retrieve it. When you're sure that you no longer need anything out of the Trash, you can empty the trash — permanently deleting files. The following list gives you some quick tips for using the KDE version of the trash can:

- Drag a file icon from the desktop or from a KFM window and drop it on the desktop Trash icon to move the file from its original location to the Trash folder.
- Right-click a file or folder icon in a KFM window and choose Move to Trash from the pop-up menu that appears. This also moves the file or folder into the Trash folder.
- Double-click the Trash icon on the desktop to open a KFM window displaying the contents of the Trash folder.
- To recover an individual file from the Trash, open the Trash folder and then click and drag the file icon out of the KFM window and drop it on the desktop or another KFM window.
- Right-click the Trash desktop icon and choose Empty Trash Bin from the pop-up menu that appears to permanently delete all the files stored in the Trash folder.

### Putting files through the shredder

If you want to remove files or folders from your system without going through the two-step process of moving them to the Trash and then emptying the Trash, KFM enables you to do just that with its Delete command. But be careful, and be very sure that you really want to erase the file or folder. The Delete command is permanent. Using delete is kind of like running a paper through the shredder instead of just dropping it into the trash bin — there's no going back and retrieving the deleted file later.

Deleting a file or folder with KFM is easy. Just follow these steps:

1. Open a KFM window and navigate to the directory containing the file or folder you want to delete.
    - You can also delete files and folders from the desktop without opening a KFM window.
2. Right-click the file or folder icon and choose Delete from the pop-up menu that appears.
    - The KFM Warning box appears as shown in Figure 4-12. This is your last chance to change your mind before permanently removing the selected file from your system.

![](img/8dd43d91b80664e771e0c0a824d7392d_101_0.png)
