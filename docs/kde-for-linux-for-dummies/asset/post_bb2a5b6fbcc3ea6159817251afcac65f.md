
- Click a right-pointing arrow to expand the tree listing and show the subdirectories nested below the directory.
- Click a down-pointing arrow to collapse the tree listing and hide any sub-directories.
- Click a directory name in the tree listing to display the contents of that directory in the main panel on the right side of the KFM window.
- The open file-folder icon beside a directory name indicates the selected directory.

When you select a directory in the tree list, KFM displays the contents of the selected directory in the right side of the KFM window. However, if you click a folder name in the right side of the KFM window, click the Home button on the toolbar, or use any other navigation technique to change directories, KFM doesn’t necessarily update the tree list to indicate which directory is open. *Don’t rely on the tree list to show the location of the current directory unless you activate the Tree View Follows Navigation option.*

- Use the scroll bar on the right side of the tree display to scroll through the tree listing.
- Right-click a directory name in the tree list to open a pop-up menu of options that enable you to do things such as open, copy, and delete the directory. Most of your options for manipulating directories in the main panel of the KFM window are also available on this pop-up menu.

The KFM directory tree panel includes a top-level branch labeled My Home and another top-level branch labeled *Desktop*. These are links to your home directory ( `/home/username` ) and Desktop subdirectory ( `/home/username/Desktop` ) rather than real branches on the directory tree. They appear on the tree list to provide convenient access to these oft-used directories so you don’t have to expand the Root branch in order to drill down to your home directory and Desktop. Note that your home directory is labeled My Home instead of its real path name.

## Showing thumbnails

If you work with a lot of image files, you’ll appreciate the way KFM displays thumbnail previews of each image in Icon View. For identifying images, a picture — even a small one — almost always beats the most descriptive file name.

To activate thumbnails, choose View:Show Thumbnails. Then, when you view the contents of a folder that contains image files, KFM displays a small preview image of each image file instead of the normal generic file icon, as shown in Figure 4-6. The Show Thumbnails command is a toggle — to deactivate it, just choose the same command again.

![](img/8dd43d91b80664e771e0c0a824d7392d_93_0.png)

**Figure 4-6: Thumbnails enable you to preview image files.**

The Show Thumbnails option works only with the large icons in Icon View, not the small icons in Long View or Short View. The small icons in the other views are too small to make useful preview images anyway. Also, before KFM can display a thumbnail preview, the image must be in a file format KFM can display at the appropriate size for an icon. If KFM can't display a file's image format (or can't adjust the image to icon size), the program displays the generic file icon for the file type instead of a thumbnail image.

### Revealing hidden files

When you view the contents of a directory in KFM, typically you see only a portion of the files and subdirectories stored there. In addition to the files you see in the normal directory listing, some directories contain many more files and subdirectories that remain invisible — hidden from view.

On a UNIX-style operating system, file and directory names that start with a period are omitted from normal directory listings. As a result, these files are effectively hidden. Often configuration files and other system files or directories are hidden in this way, especially when stored in the same directories as documents and other files that a user routinely accesses. Although hiding files can enhance security somewhat, the real purpose of hidden files isn't to keep those files secret. Hiding configuration and system files simply reduces the on-screen clutter in your directories so you don't have to look through a bunch of seldom-used configuration files in order to locate your programs and documents.

KFM normally keeps hidden files out of sight and doesn't display the file-names or icons for hidden files or directories in the main KFM window or in the tree panel. However, *if* you need access to those hidden files, you can choose **View > Show Hidden Files** to force KFM to reveal all. When you enable the **Show Hidden Files** option, KFM displays *all* the files and subdirectories in the current directory, including the “dot” files. Previously hidden directories also become visible in the directory tree panel if it is active. Figure 4-7 shows a KFM window with hidden files visible. Compare it to Figure 4-5, which shows the normal view of the same directory.

![](img/8dd43d91b80664e771e0c0a824d7392d_94_0.png)

## Peeking inside archive files

Traditionally, backup copies of files are stored in the UNIX tape archive (`.tar`) or compressed tape archive (`.tar.gz`) formats, which condense the data and file descriptions from multiple original files into each archive file. But archive files aren't just for backups any more. Archives and compressed archives are also used for other purposes such as packaging all the files for a program installation into a single *tarball* (geek jargon for a `.tar` archive file) for distribution. KDE themes are distributed as compressed archives. And just about anything you download over the Internet is likely to be in a compressed archive as well.

### TECHNICAL STUFF

Of course, you need a special utility program to create an archive file. The most common command-line utility is named, appropriately enough, `tar`. A KDE utility — Archiver — provides a graphical tool for creating archive files. You can use these same tools to view the contents of archive files and extract component files from the archive and restore them to separate, individual files that you can then use just like a copy of the original.

However, you don't have to resort to using separate utilities to work with archive files. KFM can do the job. Here's how:

- **Click an archive file (with the `.tar` or `.tar.gz` extension) in a KFM window.**
  KFM opens the file and displays its contents in the KFM window. It's just like opening a folder. In fact, KFM normally displays the contents of the archive as a single folder.
- **Click the folder icon.**
  KFM displays a list of the files and subfolders contained within the archive. Figure 4-8 shows an example of KFM displaying the contents of a compressed archive file — in this case, a theme. Note the path name in the location bar. The part following the `#` character is within the archive file.

![](img/8dd43d91b80664e771e0c0a824d7392d_95_0.png)

- **Click or drag individual files to open or copy them.**
  You can do pretty much anything with the files within the archive that you can do with files in a regular folder. You can open most documents and you can copy files from the KFM window to other locations. The principal exception is running a program from an archive. In order to run a program, you must first copy the program file and its supporting files from the archive to a regular folder on your hard drive so the operating system can find and access all the necessary files.

## Changing the appearance of the file manager

As with most KDE features, you can customize the appearance of the KFM window. The preceding sections of this chapter show you how to change the view, show thumbnails, and add the tree panel to the KFM window. But that's not all you can do. Check out these configuration options:

![](img/8dd43d91b80664e771e0c0a824d7392d_96_0.png)

- Choose **Options→Show Menubar** to remove the menus from the KFM window.

There is no easy way to restore the menu bar to a KFM window after you turn it off. Your best bet is to close the menuless KFM window and open another KFM window with its default settings intact.

- Choose **Options→Show Statusbar** to remove the status bar from the bottom of the KFM window. Choose the command again to restore the status bar.
- Choose **Options→Show Locationbar** to toggle the Location bar (the one with the big Location or address box) on or off.
- Choose **Options→Show Toolbar** to remove the toolbar from the KFM window. Choose the command again to restore the toolbar.
- Choose **Options→Configure File Manager** to open the KFM Configuration dialog box. The settings on the Font and Color tabs enable you to select the fonts and colors KFM uses to display file lists in the KFM window.

![](img/8dd43d91b80664e771e0c0a824d7392d_96_1.png)

The most interesting settings are on the Other tab, shown in Figure 4-9. There you can specify the default programs to use as your terminal emulator and text editor. Another useful setting is the Tree View Follows Navigation option. Select this option to force KFM to automatically update the Tree panel to show the current directory selection, even when you navigate to a different directory by clicking a folder in the right panel of the KFM window. (Personally, I don't understand why this option isn't enabled by default. It should be!) After adjusting the settings, click OK to close the KFM Configuration dialog box and apply the settings.
