
## Table 4-2. Nautilus keyboard shortcuts.

| Keyboard combination | Action |
|---|---|
| Alt+left cursor | Move back in the file browsing history |
| Alt+right cursor | Move forward in the file browsing history |
| Alt+up cursor | Switch to the parent folder of the one you're currently in |
| Alt+Home | Switch to the user's /home folder |
| F5/Ctrl+R | Refresh the file listing, showing any changes made since the listing appeared |
| Ctrl+=/Ctrl++ | Zoom in (show more details) |
| Ctrl+- | Zoom out (show fewer details) |
| Ctrl+0 (zero) | Zoom to default level |
| Ctrl+W | Quit file browsing window |
| Shift+Ctrl+W | Quit ALL file browsing windows |
| Ctrl+N | New browsing window |
| Ctrl+D | Add current location as bookmark |
| Ctrl+B | Edit bookmarks |
| Ctrl+T | New tab (Ubuntu 8.10 and above) |
| Ctrl+A | Select all files |
| F2 | Rename selected file/folder |
| Ctrl+O | Open selected file/folder |
| Ctrl+I/Alt+Enter | Show properties of selected file/folder |
| Ctrl+Shift+N | Create new folder |
| Delete | Move selected item to Wastebasket (Trash) |
| Shift+Delete | Permanently delete selected item (bypass Wastebasket) |
| F9 | Show/hide side pane |
| Ctrl+1 | Switch to icon view |
| Ctrl+2 | Switch to list view |
| Ctrl+3 | Switch to compact view (Ubuntu 8.10 and above) |
| Ctrl+H | Show/hide hidden files |
| Ctrl+L (or hit forward slash) | Go to location (effectively, switch to text-based location bar rather than button mode; hit Esc to switch back) |

Files can be dragged and dropped between tabs. To do so, drag the file or folder to the other tab, and Nautilus will switch to it automatically. Then release the mouse button. Alternatively, you can simply copy, cut and paste files in the usual way using the Edit menu.

## Searching for files

Ubuntu offers two methods of searching for files: using the system-wide Tracker tool, as detailed in the *Desktop Search* section in Chapter 3, or using Nautilus’ own more humble file search function. The two methods are independent, and you don’t need to have Tracker enabled to use Nautilus’ search functionality.

To use Nautilus’ search function, click the SEARCH button on the toolbar, or hit Ctrl+F. Type part of the filename you’re looking for and hit Enter. By clicking the plus sign icon in the list of results, you can further refine the search results by filtering by file type.

> **TIP**  Nautilus also offers a quick and dirty search function for files in the current folder—just ensure the Nautilus window is the active window and simply start typing. A small search text field will appear at the bottom-right of the window, and files/folders will automatically be matched and selected as you type.

## Special browsing locations

Nautilus isn’t limited to your computer’s filesystem. It is also able to browse FTP sites, and Windows shares (known as *SMB/Samba shares*). Click Go ➔ Location, and type the address of the computer you wish to connect to, preceded by either `smb://`, for Windows shares, or `ftp://`, for an FTP site.

For example, to connect to a computer that’s sharing files on the network called `office_pc`, I type `smb://office_pc`. To connect to an FTP site with the address `ftp.example.com`, I type `ftp://ftp.example.com`. Once the connection is made, you will be prompted for any username and/or password information.

Alternatively, for network shares you can click Go ➔ Network and Nautilus will attempt to detect any shared resources nearby.

> **NOTE**  Nautilus can also connect to SFTP sites too. Simply replace `ftp://` with `sftp://`, followed by the address.

## File Associations

Double-clicking certain files will cause them to open in appropriate applications. Double-clicking a movie file, for example, will open it in

Totem Movie Player. To open a file in an alternative application of your choice, right-click it and select Open with Other Application from the menu. Select the application from the list and click OPEN.

To change permanently the default application for all files of a certain type, right-click any file of that type and select Properties from the menu. Then, in the dialog box that appears, click the Open With tab, and select the radio button alongside the correct entry in the list. Click the ADD button to add an application to the list if it isn’t shown. Click the CLOSE button when done.

## File compression

For most everyday users, file compression is the process of taking many files and combining them into a single archive file that’s shrunk so it takes up less disk space. This makes the files easier to transfer from computer to computer.

Most Windows users make heavy use the Zip file format, and this is fully supported in Ubuntu.

Double-clicking a compressed file of virtually any format will open it in the FileRoller program, which is a little like WinZip under Windows. To extract any file or folder within the archive, simply click and drag it to a new location.

To create a compressed file from a file or folder, just right-click it and select the Create Archive option. Select the compression type you’d like to use from the dropdown list alongside the filename.

> TIP There’s one popular compression format missing from Ubuntu: rar. To add rar compressed file support to Ubuntu, install the rar and unrar software packages. Software installation is discussed in Chapter 6. Be aware that neither of these two software packages are Free Software, and that the rar software is a 40-day shareware demo—see the package description when installing to learn how to register.

Although Zip is popular on Windows, and there is no reason why it can’t be used under Ubuntu, most Ubuntu and Linux users prefer a different type of compression: compressed tar files.

Tar has its roots in magnetic tape backup, hence the name: Tape ARchive.

A tar file is simply lots of files combined into a single large file. Tar files aren’t compressed by default, which is to say, tar is not a compression
