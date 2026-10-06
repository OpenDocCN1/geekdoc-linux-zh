
## Part I: Getting Started in Fedora and RHEL

## Using keystrokes

If you don't happen to have a mouse or you just like to keep your hands on the keyboard, there are several keystroke sequences you can use to navigate the desktop. Here are some examples:

- Step through windows (Alt+Tab) — To step through each of the windows that are running on the desktop, hold down the Alt key and press the Tab key until you see the one you want. Release the Alt key to select it.
- Open Run command (Alt+F2) — To open a KRunning on the desktop that lets you type a command and run it, hold the Alt key and press F2. Next, type the command in the box and KRunning runs with matching commands as you prefer. Either click the command or press Enter after typing the command you want to run. You can also type a URL into this box to see a web page.
- Close the window (Alt+F4) — To close the current window, press Alt+F4.
- Close another window (Ctrl+Alt+Esc) — To close another window, press Ctrl+Alt+Esc. When a skull and cross appears as the pointer, move the pointer over the window you want to close and click the left mouse button. (This is a good technique for locking a window that has no borders or menu).
- Switch virtual desktops (Ctrl+F1, F2, F3, or F4) — To step through virtual desktops, press and hold the Ctrl key and press F1, F2, F3, or F4 to go to desktop one, two, three, or four, respectively. You could do this for up to eight desktops.
- Open window operation menu (Alt+F3) — To open the operations for the active window, press Alt+F3. When the menu appears, move the arrow keys to select an action (Move, Size, Minimize, Max, and so on), and then press Enter to select it.

## Managing files with Dolphin and Konqueror File Managers

With KDE 4.1, the KDE desktop offers two file managers: the new Dolphin File Manager and the existing Konqueror File Manager/Browser. Dolphin is a streamlined file manager that is now used by default when you open a folder in KDE. Konqueror can handle a wide range of content from local files and folders to remote content.

> For further information on Dolphin, refer to the Dolphin File Manager page (http://enzoros.gmxhome.de).

The Konqueror File Manager/Browser helps elevate the KDE environment from just another X window manager to compete with GUIs from Apple Computing or Microsoft. The features in Konqueror rival those offered by other user-friendly desktop systems. Figure 3-19 shows an example of the Konqueror File Manager window.

## Chapter 3: Getting Started with the Desktop 121

Some of Conqueror's greatest strengths over earlier file managers are the following:

- Network desktop — If your computer is connected to the Internet or a LAN, features built into Conqueror let you create links to files (using FTP) and Web pages (HTTP) on the network and open them within the Konqueror window. These links can appear as file icons in a Conqueror window or on the desktop. When a link is opened (single-click), the contents of the FTP site or Web page appears right in the Konqueror window. Given proper folder permission, you could drag and drop files to your FTP server in this.

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_168_0.png)

**Figure 3-19:** Conqueror provides a network-ready tool for managing files.

- Web browser interface — The Conqueror interface works like Firefox, Internet Explorer, or any other browser in that you select files, directories, and Web. You can open Web content by typing Web-style addresses in a Location box.

> TIP: Web pages that contain Java content will run by default in Conqueror. To double-check that Java is supported, choose Settings -> Configure Conqueror. From the Settings window, click Java & JavaScript and select the Java tab. To enable Java, click the Enable Java Globally box and click Apply. Try a game from Java.com to see if Java is working. If you need a later version of Java Runtime Environment (JRE), you can download it from http://www.java.com/en/download. After downloading the new JRE, change Path to Java Executable to /usr/java/jre1.0.

- File types and MIME types — If you want a particular type of file to always be launched by a particular application, KDE already has dozens of MIME types defined that automatically detect particular file and data types. There are MIME types defined for audio, image, video, and a variety of other content. Of course, you can also perform many file manager functions with Konqueror. For manipulating files, you can use features such as Select, Move, Cut, and Delete. You can search for files, create new items (files, folders, links), view histories of the files you have opened, and create bookmarks.

## Working with files

Because most of files in both Konqueror and Dolphin are intuitive, I will give you a quick rundown of how to do basic manipulation:

- Open file — Click a file. The file will open in the Konqueror or Dolphin window, which is the default set for the file type.
- Choose application — Right-click a file. The menu that appears shows which applications set to open it.
- Delete file — Right-click and move to Trash. If you want to permanently delete a selected file, use Shift+Delete. Just keep in mind that you won't be able to restore it from Trash if you change your mind.
- Copy a file — Right-click and select Copy. This copies the file to your clipboard. After that you can paste it to another folder. Click the Klipper (clipboard) icon in the panel to see a list of copied files.
- Paste a file — Right-click an open area of a folder and select Paste. The file you copied is pasted in the current folder.
- Move a file — With the original folder and target folder open on the desktop, press and hold the mouse button on the file you want to move, drag it to an open area of the new folder, and release the button. You could also copy or create a file using this method.
- Link a file — Drag and drop a file from one folder to another. When the menu appears, click Link. This lets you access a file from a new location without having to make a copy of the original file. When you open the link, the pointer to the original file causes it to open.

There are also several features for viewing information about the files and folders in Konqueror and Dolphin. With the addition of Dolphin to KDE 4.1, some manager features that were once available in Konqueror have been moved to the more streamlined Dolphin file manager. The following items include file management features supported by both two applications:

- View quick file information — Right-click a file in a Konqueror or Dolphin window and select Properties. A pop-up window appears with information about the item, its filename, file size, modification time and file type.
- View hidden files — In Konqueror or Dolphin, select View → Hidden Files. This allows you to see files with a dot (.). Dot files tend to be used for configuration and don't generally need to be viewed in your daily work.
- Change icon size — In Dolphin, select View → Zoom In to make the file and folder icons bigger (or Zoom Out to make them smaller).
- Change view — In Konqueror or Dolphin, select View → Mode, and then view the folder contents as icons, details, or columns.

To act on a group of files at the same time, there are a couple of actions you can take: select a group of files, click in an area of the folder and drag the pointer over the files you want. All files within the box will be highlighted. In Dolphin, you can also Edit → Select All to select all files in a folder. When they are highlighted, you can move, copy, or delete the files as described.

## Searching for files with Dolphin and kfind

If you are looking for a particular file or folder, the Find feature that was previously part of Konqueror can now be launched from Dolphin. To open a file from a Dolphin file manager, choose Tools → Find File and the window will appear. You could also start the Find/Folders window by typing kfind from a terminal. Figure 3-20 shows the Find/Folders window.

Simply type the name of the file you want to search for (in the Named text box) and the folder, including all subfolders, you want to search (in the Look text box). Then click the Find button. Use wildcards, if you like, with your search. For example, search for *.rpm or * to find all files that end in .rpm or * to find all doc files. You can also select to have the search be case sensitive or click the Help button to get more information on searching.

To limit your search, you can click the Properties tab, and then enter a date range (between), a number of months before today (the previous x months), or the number of days before today (the previous x days). Select the Contents tab to limit the search to files of a particular type (of Type), files that include text that you enter (Containing Text), or that are of a certain size (Size is) in kilobytes.
