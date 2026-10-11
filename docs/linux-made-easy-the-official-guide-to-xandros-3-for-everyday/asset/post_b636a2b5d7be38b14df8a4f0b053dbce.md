
## Creating a ZIP File

The procedure for creating a ZIP archive is essentially the same as that for creating a tarball: create a new folder, copy or move all the files you want to place in the archive in that folder, right-click the folder, and select **Add to ZIP Archive** in the pop-up menu. Once you've completed those steps, an *Add to Zip Archive* window (Figure 5-8) will appear with the name of the folder you're archiving given as the name of the soon-to-be-created ZIP file. Assuming that name will do, all you have to do is click **OK**, and the process will be complete within a few seconds—maybe less. If, however, you suddenly remember that you forgot to add a certain file to the archive, you can choose to add it at this point (before clicking **OK**).

![](img/3badae5570de77b990135448f8a8a1cc_96_0.png)

*Figure 5-8: Creating a ZIP archive*

To add a file to your under-construction ZIP archive, click the **Add** button in the bottom half of the Add to Zip Archive window. Another window, *Add files or folders*, will then appear, and from that window you can choose other files to add. Once you have found the file you want to add, select it and then click **Open**. The file you choose will then appear in the list at the bottom of the Add to Zip Archive window. To add yet another file, repeat this procedure again. Once you have finished adding files, click **OK**.

What if you want to add files after the ZIP archive is already created? Well, just treat the archive like a regular folder and do a copy-and-paste routine. Here's what you would do, step-by-step:

- 1. Select the file (or files) you want to add to an existing ZIP archive, right-click it (or them), and then select **Copy** in the pop-up menu.
- 2. Next, double-click the ZIP archive you will be adding to.
- 3. When the window for that archive opens, right-click any open space within that window, and then select **Paste** in the pop-up menu.

## Xandros File Manager as an Image Viewer

Another one of the handy things about XFM is that it can act as a sort of picture viewer and previewer. If you click once on any graphics file, a thumbnail of that file will appear in the left side of the right pane of the XFM window, as you can see in Figure 5-9.

![](img/3badae5570de77b990135448f8a8a1cc_97_0.png)

Figure 5-9: Viewing a thumbnail of an image file in an XFM window

You can also have your graphics files appear as thumbnails, rather than icons (as shown in Figure 5-10), by going to the View menu and selecting Thumbnails. This lets you see your graphics files without having to use any other special imaging software. Admittedly, this feature is no longer unique in the world of operating systems, but it is handy nonetheless. What is more unique to Xandros, you will learn shortly, is that same functionality works for text files too.

When you double-click a thumbnail of an image in XFM, that image will appear at a larger size in the right pane of the XFM window (Figure 5-11). At the same time, a set of controls will appear with which you can browse through your images at an enlarged size, rotate them, adjust the level of magnification, or even run an in-window slideshow. This is all very cool, especially for a mere file manager.

![](img/3badae5570de77b990135448f8a8a1cc_98_0.png)

![](img/3badae5570de77b990135448f8a8a1cc_98_1.png)

If you would like to see an image at a size beyond the constraints of the right pane of the XFM window, you can do so by right-clicking the thumbnail of the image in question and selecting **Open With > Image Viewer** in the pop-up menu. The image will then appear in its own window, as you can see in Figure 5-12. In Image Viewer (also called KView), not only do you have all the viewing options you do when viewing images in an XFM window, but you can also have your images fill the entire screen by selecting **Full Screen Mode** in the Settings menu and then selecting **Fit Image to Window** in the View menu. To get back to normal, just go to the Settings menu again and select **Exit Full Screen Mode**.

![](img/3badae5570de77b990135448f8a8a1cc_99_0.png)

### Using XFM to View Text and PDF Files

In addition to letting you view graphics files, the Xandros File Manager allows you to read the contents of text files (those saved with a .txt file format), again without the need for any other software. If, for example, you have some notes that you jotted down and saved as a text file, you can simply double-click the file’s icon in the right pane of the XFM, and the file’s contents will be displayed in the XFM window. XFM can even do the same for PDF files, acting as a simple PDF viewer. Just clicking a text or PDF file will even give you a small preview of that document in the left-hand side of the XFM window, as is the case with graphics files.

Of course, you can always opt to read a PDF file in a window of its own by right-clicking the PDF file you want to view and selecting **Open With** » **Acrobat Reader** in the pop-up menu (Figure 5-13), or, if Acrobat Reader doesn't seem to do the trick, **Open With** » **PostScript Viewer**. Text files can be read in a similar fashion by selecting **Open With** » **Text Editor**.

![](img/3badae5570de77b990135448f8a8a1cc_100_0.png)

*Figure 5-13: Viewing a PDF file in Acrobat Reader*

## Changing File and Folder Permissions Within XFM

You will find, as you make your way along in the Linux world, that occasionally you come across a file that your system will not allow you to alter. When you open up such a file in the appropriate application, the title bar will often say *Read Only*, or when you try to save the file, you will get a *Permission Denied* message. Messages of this type are telling you that the file is write-protected, meaning that you do not have permission to alter the file. In all likelihood, the only time you will encounter this situation in Xandros is when you copy files from a CD to your hard disk or when you copy files from your Windows partition to your Linux partition. This is another way that Linux tries to protect you from harming your system, though in the case of copied CD files, it may not be clear to you how it’s protecting you.

If you want to alter a file or gain access to a folder that is write-protected, it is possible to do so in an XFM window as long as you are listed as the owner of that file or folder. To change file or folder permissions, just right-click the file or folder in question and then select **Properties** from the pop-up menu.

Once the Properties window opens, click the **Permissions** tab, and you will see who the owner of the file or folder is and what you are allowed or not allowed to do with it (see Figure 5-14).

![](img/3badae5570de77b990135448f8a8a1cc_101_0.png)

> *Figure 5-14: Changing permissions in an XFM Properties window*

As you can see in Figure 5-14, permissions can be granted or denied to the *owner* of the file or folder (you), to a specified *group*, or to *others* (everybody else). These permissions are:

- **Read**
  - Permission to view the contents of a file or folder
- **Write**
  - Permission to alter the contents of a file or folder
- **Execute**
  - Permission to run a program or script

In general, you needn’t worry all that much about setting permissions for your own files, because you are really the only one who has access to your user account. The main exception to this is when you transfer files from a CD to your hard disk. In this case, the files likely will be write-protected, meaning that you cannot alter the files until you change their permissions.

If you are dealing with a write-protected folder or file, you can change the file’s permissions to allow you to alter it by clicking the checkbox under the word *Write* in the *Owner* row. Once you have finished, click **OK** and you’ll be free to do what you like with that file.

## Using XFM with Your Windows Partition (for Dual-Booters Only)

If you set up a dual-boot system when you installed Xandros, you can also get read-only access to the files in your Windows partition, but not the programs, via the Xandros File Manager. To do so, follow these steps:

- 1. Click the C: icon in the file tree in the left pane of the XFM window (or whatever drive contains the files you want). The contents of your Windows C: drive should appear on the right-hand side of the right pane of the XFM window (Figure 5-15).

  > **NOTE** You still only have read access to the partition (see the left-hand side of the XFM window, which tells you this), which means you can copy files from, but not to, the Windows partition. Although this may seem a bit inconvenient, it is probably best in the long run, because it protects the integrity of your Windows system and can help to prevent any problems from occurring the next time you decide to boot up in Gatesville.

  ![](img/3badae5570de77b990135448f8a8a1cc_102_0.png)

  *Figure 5-15: Getting read-only access to your Windows files*

  > **NOTE** Assuming your files are stored, as most people's are, in your Windows *My Documents* folder, you can access them by double-clicking the *Documents and Settings* folder.

- 2. Once the contents of that folder appear in the right pane, look for the folder with your Windows username (mine says rg) and then double-click that folder.
