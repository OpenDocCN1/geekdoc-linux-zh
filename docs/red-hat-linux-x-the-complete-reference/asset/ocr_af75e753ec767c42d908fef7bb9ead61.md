# KDE File Manager and Internet Client: Konqueror

The KDE file manager, known as Konqueror, is a multifunctional utility with which you can manage files, start programs, browse the Web, and download files from remote sites (see Figure 7-4). Traditionally, the term "file manager" was used to refer to managing files on a local hard disk. The KDE file manager extends its functionality well beyond this traditional function because it is Internet capable, seamlessly displaying remote file systems as if they were your own, as well as viewing Web pages with browser capabilities. It is capable of displaying a multitude of different kinds of files, including image, PostScript, and text files. KOffice applications can be run within the Konqueror window. You can even open a separate pane within a file manager window to run a terminal window where you can enter shell commands (Window menu).

![](bbox=[0.15, 0.43, 0.55, 0.68])

Figure 7-4: The KDE file manager

# Konqueror Window

A KDE file manager window consists of a menu bar, a navigation toolbar, a location field, a status bar, and a sidebar that provided different views of user resources such as a tree view of file and directory icons for your home directory. When you first display the file manager window, it displays the file and subdirectory icons for your home directory. Files and directories are automatically refreshed. So if you add or remove directories, you do not have to manually refresh the file manager window. It automatically updates for your listing, showing added files or eliminating deleted ones. The files listed in a directory can be viewed in several different ways. You can view files and directories as icons, as small icons, or in a detailed listing. The detailed listing provides permissions, owner, group, and size information. Permissions are the permissions controlling access to this file (see Chapter 28). Configuration files, known as hidden files, are not usually displayed. To have the file manager display these files, select Show Hidden Files from the View menu. Konqueror also supports split views, letting you view different directories in the same window (Windows menu). You can split vertically or horizontally.

You can open a file either by clicking it or by selecting it and then choosing the Open entry in the File menu. If you want to select the file or directory, you need to hold down the CTRL key while you click it, or single-click. A double-click opens the file. If the file is a program, that program starts up. If it is a data file, the associated application is run using that data file. For example, if you double-click a text file, the Kate application starts displaying that file. If Konqueror cannot determine the application to use, it opens a dialog box prompting you to enter the application name. You can click the Browse button on this box to use a directory tree to locate the application program you want.

The file manager can also extract tar archives and install RPM packages. An archive is a file ending in .tar.gz, .tar, or .tgz. Clicking the archive lists the files in it. You can extract a particular file simply by dragging it out the window. Clicking a text file in the archive displays it with Kate, while clicking an image file displays it with KView. Selecting an RPM package opens it with the redhat-config-packages utility, which you can then use to install the package.

# Navigation Panel

The navigation panel is a sidebar that lists different resources that a user can access with Konqueror. You