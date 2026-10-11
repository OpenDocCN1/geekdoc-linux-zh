
## The File Manager

The File Manager (dtfile) provides a graphical means of manipulating files and directories with your mouse and keyboard. The program is a file browser that is similar in function to the Macintosh Finder or the Windows Explorer. Earlier in this chapter (in the section “Windows”), the Window menu and elements of the File Manager window were described. In this section, I’ll describe the File, Selected, View, and Help menus, as well as how to work with window content.

> **NOTE** Chapter 5, “The File System,” describes using the File Manager to perform numerous file management tasks. There is some overlap between the topics described in this section and that chapter; this section describes the interface features of the File Manager.

There are two ways to open the File Manager:

- Click the Home Folder icon on the front panel.
- In a terminal window, enter the command **dtfile**.

In both instances, you open a File Manager window with the home folder contents showing. The **dtfile** command takes numerous options you can use to specify which folder or directory to open and the size and condition of the window spawned. You should use the **-folder** [**<foldername>**, ...] or **-dir** [**<foldername>**, **<foldername>**, ...] option to open a specific folder window (or set of folder windows, one for each folder name specified). Among the other options are those that let you rename the title bar (**-title**), suppress the display of folders above a restricted folder (**-restricted**), turn a grid on or off (**-grid** on/off), display a file tree (**-tree_files**), and change the icon attributes (**-order**, **-view**, **-direction**), and various icon size parameters. The man **dtfile** pages contains extensive notes on this command.

Tables 7.6 through 7.9 describe the actions of each of the commands found in the Workspace menu submenus (File, Selected, View, and Help). What you see on the menus described in these tables depends upon whether the content you are looking at is from a drive, diskette, or CD-ROM and also the type of files and folders selected.

### TABLE 7.6: THE FILE SUBMENU COMMANDS

| Command Name | Keystroke | Description |
| :--- | :--- | :--- |
| New Folder | No keystroke | Opens the New Folder dialog box. Enter a name into the New Folder Name text box, then click the OK button to create a folder with that name within your current folder. |
| New File | No keystroke | Opens the New File dialog box. Enter a name into the New File Name text box, then click the OK button to create a data file with that name within your current folder. A data file has a blank page icon. |
| Go Home | Ctrl+H | Opens your home directory in your current window. |
| Go Up | Ctrl+U | Moves your window view up one level in the file hierarchy. |
| Go To | No keystroke | Opens the Go To dialog box. Select a name from the System Name list box, enter a /pathname>/<foldername> into the Destination Folder text box, then click the OK button to move the view of your current window to the folder with that name within your current folder. |
| Find | Ctrl+F | Opens the Find dialog box, which you can use to search for files and folders locally, on the network, and elsewhere. |
| Open Terminal | Ctrl+T | Opens a terminal window so that you can execute commands from the command line. |
| Open Floppy | No keystroke | Opens the contents of a diskette in a window. |
| Open CD-ROM | No keystroke | Opens the contents of a CD-ROM in a window. |
| Eject | No keystroke | Ejects a diskette or CD-ROM. |
| Format Floppy | No keystroke | Opens the Format Floppy dialog box, which you can use to format a diskette. |
| Rename Floppy | No keystroke | Allows you to rename a diskette’s volume label. |
| Close | Alt+F4 | Closes the current File Manager window. |

### TABLE 7.7: THE SELECTED SUBMENU COMMANDS

| Command Name | Keystroke | Description |
| :--- | :--- | :--- |
| Move To | No keystroke | Opens the Move Object dialog box. Enter a /pathname>/<foldername> into the Destination Folder text box, then click the OK button to move a selected item to that folder. |
| Copy To | Ctrl+C | Opens the Copy Object dialog box. Enter a /pathname>/<foldername> into the Destination Folder text box, a file-name into the Name for Copy text box, then click the OK button to move a selected item to that folder. |
| Copy as Link | No keystroke | Opens the Link Object dialog box. Enter a /<path name>/<folder name> into the Destination Folder text box, a file-name into the Name for Copy text box, then click the OK button to move a selected item to that folder. |
| Rename | No keystroke | Places an insertion point into the selected file or folder’s name. Type a new name and press the Return key to rename the object. |
| Put in Workspace | No keystroke | Puts a symbolic link to the selected file or folder on the desktop backdrop in the upper-right corner of your screen. You can control the default placement of the icon with the objectPlacement resource. |
| Put in Trash | No keystroke | Moves the selected file(s) or folder(s) to the Trash Can folder. |
| Properties | Ctrl+Backspace | Opens the Properties dialog box, which shows permissions and information for a selected file or folder. |
| Select All | Ctrl+/ | Selects all objects in the File Manager window. |
| Deselect All | Ctrl+\ | Deselects all objects in the File Manager window. |
| Open | No keystroke | Opens a selected object. |
| Print | No keystroke | Grayed out unless a file is selected. Opens the Print dialog box. |
| Open in Place | No keystroke | Opens a view containing the contents of a folder, diskette, or CD-ROM in the currently open File Manager window. |
| Open in New View | No keystroke | Opens a new File Manager window that contains the contents of the selected folder. (A similar command appears in the View menu for some content.) |

### TABLE 7.8: THE VIEW SUBMENU COMMANDS

| Command Name | Keystroke | Description |
| :--- | :--- | :--- |
| Open New View | No keystroke | Opens another window showing the contents of the current folder. |
| Set View Options | No keystroke | Opens the Set View Options dialog box, which allows you to control what you see in a File Manager window. |
| Save as Default Options | No keystroke | Saves the view options you selected so that the next time you open this folder, it appears the same way. |
| Show Hidden Objects | Ctrl+S | Displays hidden objects (objects whose data types have been set to Hidden in the Set Filter Options dialog box). |
| Set Filter Options | No keystroke | Opens the Set Filter Options dialog box, which you can use to hide or show files of different data types. |
| Clean Up | No keystroke | Moves your icons to a row and column display if you have the option set for window behavior to leave icons in the window where you place them. |
| Update | No keystroke | Refreshes your view of a window’s contents. |

### TABLE 7.9: THE HELP SUBMENU COMMANDS

| Command Name | Description |
| :--- | :--- |
| Overview | Opens the File Manager Help window to an outline or overview of the topics. |
| Table of Contents | Opens the File Manager Help window to a listing of topics in the help system. |
| Tasks | Opens the File Manager Help window to a listing of topics about the File Manager tasks. |
| Reference | Opens the File Manager Help window to reference summaries about components of the CDE desktop. |
| On Item | Changes your cursor to a question mark. Click an object or menu for which you want information and the File Manager Help window opens to a description of that object. |
| Using Help | Opens the File Manager Help window to a short description of how to use the help system. |
| About File Manager | Displays the copyright information for the Common Desktop Environment. |

There are several ways to move about the directory hierarchy. To open a folder, you can double-click it in the iconic path or you can double-click it in the File Manager window. If you click the text box to the right of the iconic path, you can enter the path to the folder you want to open and then press the Return key to view the contents of that folder in your window.
