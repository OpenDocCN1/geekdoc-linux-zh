
Figure 3-16: Konqueror provides a network-ready tool for managing files.

![](img/27a85d56d393921ced6412ae6e8336bf_131_0.png)

- **Web browser interface** — The Konqueror interface works like Mozilla, Internet Explorer, or another Web browser in the way you select files, directories, and Web content. A single-click opens a file, link to a network resource, or application program. You can also open content by typing Web-style addresses in a Location box.

> **TIP:** Web pages that contain Java content will not run by default in Konqueror. To turn on Java support, choose Settings → Configure Konqueror. From the Settings window, click Java & JavaScript and select the Java tab. To enable Java, click the Enable Java Globally box and click Apply.

- **File types and MIME types** — If you want a particular type of file to always be launched by a particular application, you can configure that file yourself. KDE already has dozens of MIME types defined that can automatically detect particular file and data types and start the right application. There are MIME types defined for audio, image, text, video, and a variety of other content types.

Of course, you can also perform many standard file manager functions with Konqueror. For manipulating files, you can use features like Select, Move, Cut, Paste, and Delete. You can search directories for files, create new items (files, folders, and links, to name a few), view histories of the files and Web sites you have opened, and create bookmarks.

## Working with files

Because most of the ways of working with files in Konqueror are quite intuitive (by intention), I’ll just give a quick rundown of how to do basic file manipulation:

- **Open a file** — Double-click the left mouse button on a file. The file will open right in the Konqueror window, if possible, or in the default application set for the file type. You can also open a directory (to make it the current directory), application (to start the application), or link (to open the target of a link) in this way.

- **Choose an application** — Single-click the left mouse button to highlight it or right mouse button to open a menu. When you right-click a data file, select the Open With menu. The menu that appears shows which applications are set up to open the file.

- **Delete a file** — Single-click the right mouse button and select Delete. You are asked if you really want to delete the file. Click Yes to permanently delete it.

- **Copy a file** — Single-click the right mouse button and select Copy. This copies the file to your clipboard. After that, you can paste it to another folder. (See the "Move a file" bullet for a drag-and-drop method of copying.)

- **Paste a file** — Single-click the right mouse button (on an open area of a folder) and select Paste. A copy of the file you copied previously is pasted in the current folder.

- **Move a file** — With the original folder and target folder both open on the desktop, press and hold the left mouse button on the file you want to move, drag the file to an open area of the new folder, and release the mouse button. From the menu that appears, click Move. (You could also copy or create a link to the file using this menu.)

- **Link a file** — Drag-and-drop a file from one folder to another. When the menu appears, click Link Here. (A linked file lets you access a file from a new location without having to make a copy of the original file. When you open the link, a pointer to the original file causes it to open.)

There are also several features for viewing information about the files and folders in your Konqueror windows:

- **View quick file information** — Position the mouse pointer over the file. When a mouse pointer is over a file in a Konqueror window, information appears in the window footer. This includes the filename, file size, and file type.

- **View hidden files** — Select View → Show Hidden Files. This allows you to see files that begin with a dot (.). Dot files tend to be used for configuration and don’t generally need to be viewed in your daily work.

- **View file system tree** — Select View → View Mode → Tree View. This presents a tree view of your folder, displaying folders above the current folder in the file system. You can click a folder in the tree view to jump directly to that folder. There are also Multicolumn, Detailed List, and Text views available.

- **Change icon view** — Select View → Icon Size, and then choose Large, Medium, or Small to select the size of the icons that are displayed on the window. You can also choose Default Size, to return to the default icon size.

To act on a group of files at the same time, there are a couple of actions you can take. Choose Edit → Select. A pop-up window lets you match all (*) or any group of documents indicated by typing letters, numbers, and wildcard characters. Or, to select a group of files, left-click in an open area of the folder and drag the pointer across the files you want to select. All files within the box will be highlighted. When files are highlighted, you can move, copy, or delete the files as described earlier.

## Searching for files

If you are looking for a particular file or folder, you can use the Konqueror Find feature. To open a Find window to search for a file, choose Tools → Find File. (You could also start the kfind window by typing kfind from a Terminal window.) Figure 3-17 shows the kfind window.

![](img/27a85d56d393921ced6412ae6e8336bf_133_0.png)

Figure 3-17: Search for files and folders from the kfind window.

Simply type the name of the file you want to search for (in the Named box) and the folder, including all subfolders, you want to search in (in the Look in box). Then click the Find button. Use metacharacters, if you like, with your search. For example, search for *.rpm to find all files that end in .rpm or z*.doc to find all files that begin with z and end with .doc. You can also select to have the search be case-sensitive or click the Help button to get more information on searching.

To further limit your search, you can click the Date Range tab, then enter a date range (between), a number of months before today (during the previous x months), or the number of days before today (during the previous x days). Select the Advanced tab to choose to limit the search to files of a particular type (of Type), files that include text that you enter (Containing Text), or that are of a certain size (Size is) in kilobytes.

## Creating new files and folders

You can create a variety of file types when using the Konqueror window. Choose Edit → Create New, and select one of the following types:

- **Directory** — Opens a box that lets you type in a new directory name. Type the name, click OK, and an icon representing the new directory appears.

- **Illustration Document** — Opens a box that lets you create a document in kontour format (an illustration). Type the document name you want to create and click OK. The document should have a .kil suffix if you want it to automatically open in kontour.

- **HTML File** — Opens a box that lets you type the name of an HTML file to create.

- **Text File** — Opens a box that lets you create a document in text format and place it in the Konqueror window. Type the name of the text document to create and click OK.

- **CD/DVD-ROM Device** — Opens a box that lets you type a new CD-ROM or DVD-ROM device name. Click the Device tab and type the device name (/dev/cdrom), the mount point (such as /mnt/cdrom), and the file system type (you can use iso9660 for the standard CD-ROM file system, ext2 for Linux, or msdos for DOS). When the icon appears, you can open it to mount the CD-ROM or DVD-ROM and display its contents.

- **Floppy Device** — Opens a box to type a new floppy name. Click the Device tab and type the device name (/dev/fd0), the mount point (such as /mnt/floppy), and the file system type (you can use auto to autodetect the contents, ext2 for Linux, or msdos for DOS). When the icon appears, open it to mount the floppy and display its contents.

- **Hard Disc** — Opens a box that lets you type the name of a new hard disk or hard-disk partition. Click the Device tab and type the device (/dev/hda1), the mount point (such as /mnt/win), and the file system type (you can use auto to autodetect the contents, ext2 or ext3 for Linux, or vfat for a Windows file system). When the icon appears, you can open it to mount the file system and display its contents.

- **Link to Application** — Opens a window that lets you type the name of an application. Click the Permissions tab to set file permissions (Exec must be on if you want to run the file as an application). Click the Execute tab and type the name of the program to run (in the field: Execute on click) and a title to appear in the title bar of the application (in the field: Window Title). If it is a text-based command, select the Run in terminal box. Click the box to Run as a different user and add the user name. Click the Application tab to assign the application to handle files of particular MIME types. Click OK.

- **Link to Location (URL)** — Selecting this menu item opens a box that lets you create a link to a Web address. Type a name to represent the address and type the name of the URL (Web address) for the site. (Be sure to add the http://, ftp://, or other prefix.)

- **Presentation Document** — Opens a box to create a document in kpresenter format (a presentation). Type the document name you want to create and click OK. The document should have a .kpr or .kpt suffix if you want it to automatically open in kpresenter.

- **Spread Sheet Document** — Opens a box that lets you create a document in kspread format (a spreadsheet). Type the document name you want to create and click OK. The document should have a .ksp suffix if you want it to automatically open in kspread.
