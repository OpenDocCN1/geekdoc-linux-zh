
## Figure 5-5: The Nautilus Spatial mode.

The menu bar in Spatial mode contains most of the same entries as in Browser mode. However, instead of the Go and Bookmark entries used in Browser mode, the Spatial mode menu bar uses the Places menu entry. The Places menu entry works exactly as the Places menu item in the Panel menu.

You'll notice that the bottom status bar in the Spatial mode window contains two items:

- A drop-down list of parent folders. You can select any of the parent folders in the list and jump to that location.
- Status information on the number of items and the amount of free space available in the folder.

The drop-down list is similar to the location bar in Browser mode. Clicking on the drop-down list produces a list of folders in the path of the current folder, starting at the root folder. You can select any of the folders to open a new Spatial mode window at that location.

Although Spatial mode doesn't include the View-as options, you can still switch between Icon and List view using the View menu bar item. Just select the Icon or List view items from the menu. There are also options for changing the icon or font size, just like the Zoom button in the Browser Mode window.

## Modifying Nautilus Windows

You can easily customize the look and feel of Nautilus to suit your needs. Simply select Edit → Preferences from the top menu. The main Preferences dialog box appears, as shown in Figure 5-6.

## Figure 5-6: The Nautilus Preferences dialog box.

There are six tabs in the Preferences dialog box for altering how Nautilus displays file and folder information. The following sections describe each of these tabs and the settings available on them.

### The Views Tab

The Views tab contains settings for how items appear in the View pane. It includes settings for both Icon and List views:

- View New Folders: Sets the default view to Icon or List view.
- Arrange Items: Sets how Nautilus displays icons in the View pane, either by name, size, type, modification date, or emblems added to the icon.
- Sort Folders Before Files: When checked, folders are sorted first in the View pane, by the Arrange Items setting, then files are sorted. When not checked, all items are sorted by the Arrange Item setting.
- Show Hidden and Backup Files: Displays files starting with a period or with a .tarfile extension.
- Icon Default Zoom Level: Sets the default icon size in Icon view. Set to 100 percent by default.
- Use Compact Layout: When checked, reduces the amount of space between icons in Icon View mode.
- **Text Beside Icons:** Places filename and other information next to the file or folder icon instead of beneath the icon.
- **List Default Zoom Level:** Sets the default font size in List view. Set to 50 percent by default.
- **Show Only Folders:** In the left pane in Tree mode, displays only folders in the tree, not files.

These settings affect the Nautilus window, as well as the desktop file and folder icons. Changing these settings has an immediate effect on the existing icons.

### The Behavior Tab

The Behavior tab controls how Nautilus responds to actions when clicking file icons or text in the View pane and on the desktop. The options available to set in this tab are

- **Single-Click to Open Items and Double-Click to Open Items:** Radio buttons indicate whether files open using a single-click or a double-click.
- **Always Open in Browser Windows:** When checked, Nautilus windows open in Browser mode. When not checked, Nautilus windows open in Spatial mode.
- **Run Executable Text Files When They Are Opened:** When clicking on a text file, run the file as a shell script using Terminal.
- **View Executable Text Files When They Are Opened:** When clicking on a shell script text file, open the file in a text editor.
- **Ask Each Time:** When clicking on a shell script text file, ask whether you want to run the file or open it in a text editor.
- **Ask Before Emptying the Trash or Deleting Files:** When clicking the Empty Trash button, ask before deleting files in the trash folder.
- **Include a Delete Command That Bypasses Trash:** Adds an item to the right-click menu to delete the file instead of sending to trash.

> The single-click option allows you to launch applications and open files by single-clicking rather than double-clicking. This mode can be dangerous, and you must be careful when selecting a file for copying or deleting. To select a file without opening it, hold down the Ctrl key before clicking the file.

### The Display Tab

The Display tab controls how Nautilus displays file and folder information when in Icon View mode. When Icon view is at 100 percent zoom level, by default all you see is the name of the file or folder. If you use the Zoom button (or View → Zoom from the menu bar) to zoom in closer, you see additional information about the file at different zoom values. There are three zoom levels at which Nautilus provides information about the icon item:

- The 50 percent zoom level
- The 150 percent zoom level
- The 400 percent zoom level
