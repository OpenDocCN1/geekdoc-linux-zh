
The default KDE desktop starts out with an assortment of desktop icons — mostly links to special-purpose folders (such as Autostart) and system devices (such as cdrom). However, you’re not stuck with this meager selection of icons. You can create your own desktop icons for the programs and documents you use the most. We show you how in the “Working with Desktop Icons” section of this chapter.

## Launching a program with a panel button

Icons on your desktop aren’t the only way you can instantly access your applications in KDE. You can also use panel buttons to launch programs. In addition to the KDE Menu button and the other special buttons such as the Window List, Toolbox, and virtual desktop buttons, the KDE panel is home to an assortment of buttons for individual applications and utilities.

When you install KDE, it typically starts out with the panel that is populated with a set of program buttons for utilities such as KVT, Konsole, Khelp, KCalc, KNotes, Kedit, and KMail. Like so many other things in KDE, the selection of panel buttons is customizable. You can easily remove program buttons from the panel, add buttons for other applications, and move or rearrange the buttons on the panel. We show you how in Chapter 5.

Launching a program with a panel button couldn’t be any simpler. You just click the button, and KDE instantly launches the associated application or utility. There are no menus to navigate or other selections to make — KDE just opens the program as fast as your system can access the related files.

There’s a real advantage to launching programs from panel buttons as opposed to desktop icons. Desktop icons are often obscured behind the various windows that might be open on your desktop, whereas the panel usually remains visible on top of any open windows. Having the panel always visible makes panel buttons accessible without the need to first move or minimize (iconify) windows in order to uncover desktop icons. On the other hand, this advantage may not be as pronounced if you have your panel collapsed or configured to autohide (slip out of sight when it’s not in use). If the panel isn’t visible, you need an extra mouse action to bring the panel into view before you can click a panel button to launch your application. (Collapsing and expanding the panel is covered in Chapter 1, and setting the panel to Autohide is covered in Chapter 5.)

## Instant access to typed commands

Sometimes the fastest way to launch a program is to just issue a typed command. This is especially true if you’re a veteran Linux/UNIX command line user or if you need to launch an infrequently used program for which you haven’t set up a KDE icon, button, or menu item. Of course, you could launch one of the KDE terminal emulation utilities (KVT or Konsole) and use it to interact with the operating system command line. (See Chapter 12 for more information on using the command line in a terminal window.)

Issuing commands in a terminal window works, but KDE offers a simpler alternative for issuing commands that you can type on a single line. Just follow these steps:

- **Right-click the desktop and choose Execute Command from the pop-up menu that appears.**

  KDE opens the Command box as shown in Figure 2-2.

![](img/8dd43d91b80664e771e0c0a824d7392d_57_0.png)

- **Type the command to launch your program and then press Enter.**

  KDE closes the Command box and passes the command to the operating system. Linux executes the command and launches your application. If you properly typed the command to launch a KDE or X Window program, the program window appears.

**WARNING!** Be careful with commands you type in the Command box. Any command you enter is executed immediately and, unlike typing a command in a terminal window, you won't see any error messages or other warnings that your command generates. The results of mistyping a command to launch a program are usually harmless (it doesn't work and you have to try again), but using the Command box to enter system commands or to launch command-line programs may have unpredictable results.

## Working with Desktop Icons

Desktop icons are those little symbols, such as folders and a trash can, that start out on the left side of the default KDE desktop. Chapter 1 identifies the desktop icons you find on the default KDE desktop. They include icons for the Autostart and Templates folders, the Trash folder, and the CD-ROM and Floppy drives. But, as Figure 2-3 shows, you're not stuck with that limited assortment of icons. Just as you have an assortment of tools and papers on your physical desk, you can have an assortment of desktop icons on your KDE desktop so the files, folders, and programs represented by those icons are always within easy reach.

When you click a desktop icon, the effect is the same as if you clicked the icon for the file or other resource represented by the icon — KDE launches the program and/or opens the file or folder. For example, if you click a desktop icon for a folder, KDE opens a KFM window and displays the contents of the linked folder. If you click an icon for a World Wide Web URL, KDE opens your Web browser (usually KFM), which then retrieves and displays the Web page found at the address recorded in the icon's link file. If you click a desktop icon for a text file, KDE launches your text editor and loads the text file for editing.

### TECHNICAL STUFF

How does KDE know what program to use to open your file when you click a desktop icon for a text file or other file type? It identifies the file's MIME type by its extension and uses the application that is associated with that MIME type to open the file. See Chapter 4 for information about associating specific programs with file types.

![](img/8dd43d91b80664e771e0c0a824d7392d_58_0.png)

**Figure 2-3: You can populate your desktop with a wide range of icons.**

You can create desktop icons for all sorts of files and system resources, including the following:

- **Files:** A link to any document or other file on your system. Clicking a file icon opens the file in the appropriate program.
- **Folders:** A link to a directory anywhere in the file system. Clicking a folder icon opens a KFM window displaying the contents of the folder. Of course, to use the link, the target directory must be part of a mounted file system and you must have the proper access permission.
- **File System Device:** A link to a mountable device or directory such as floppy disk, CD-ROM drive, hard disks, and file systems from other machines. Clicking a device icon opens a KFM window and displays the contents of the device — if the device is already mounted. Otherwise KDE attempts to mount the device first and displays an error message if you lack the proper permissions to mount the device.
- **FTP URL:** The Internet address for the directory on an FTP (File Transfer Protocol) server. Clicking an FTP icon launches your FTP program and attempts to access the FTP address.
- **Application:** A link to an executable program (including shell scripts). Clicking an application icon launches the program.
- **Internet Address URL:** The address for a generic Internet resource. Clicking an Internet Address icon launches the appropriate program and attempts to access the URL.
- **World Wide Web URL:** The Internet address for a Web page. Clicking a Web address icon launches your Web browser and loads the Web page.

The KDE desktop icons are actually graphic representations of link files stored in the Desktop subfolder of your home directory. The KDE link file specifies what icon to display and defines a link between the desktop icon and the file, program, or system resource the icon represents, but KDE doesn't actually store the target of the link (or even a copy of it) on your desktop.

## Arranging icons

KDE starts out with the default desktop icons arranged in a neat column on the left side of your desktop. But you don't have to leave the icons there any more than you have to leave the items on your real-world desk arranged the way they were when you first walked into your new office. You can rearrange your desktop icons any time you want.

- To move an icon, just click the icon and hold the left mouse button down as you drag the icon to a new location. Release the mouse button to deposit the icon at its new home.
