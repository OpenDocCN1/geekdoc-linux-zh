
![](img/f28adb66a7398a382f0505e0ba74a872_309_0.png)

**Figure 8-5** The Compress window

The **Edit→Backgrounds and Emblems** selection has three buttons on the left: Patterns, Colors, and Emblems. Click **Patterns** to display many pattern objects on the right side of the window. Drag and drop one of these objects on the View pane of a File Browser window to change the background of all File Browser View panes. Drag and drop the **Reset** object to reset the background to its default color and pattern (usually white). The **Colors** button works the same way as the **Patterns** button. The **Emblems** button works the same way as the **Emblems** tab in the Side pane (page 266).

The **Edit→Preferences** selection displays the **File Management Preferences** window (Figure 8-6). This window has six tabs that control the appearance and behavior of File Browser windows.

![](img/f28adb66a7398a382f0505e0ba74a872_309_1.png)

**Figure 8-6** The **File Management Preferences** window, **Views** tab

The **Views** tab sets several defaults, including which view the File Browser displays (Icon, List, or Compact view), the arrangement of the objects, the default zoom level, and default settings for the Compact view.

**Delete versus Move to Trash** The **Behavior** tab controls how many clicks it takes to open an object and what Nautilus does when it opens an executable text object (script). For more confident users, this tab has an option that includes a Delete selection in addition to the Move to Trash selection on several menus. The Delete selection immediately removes the selected object instead of moving it to the Trash folder. This tab also holds the check box labeled *Always open in browser window* that is described under “The Two Faces of Nautilus” on page 99.

The **Display** tab specifies which information Nautilus includes in object (icon) captions. The three drop-down lists specify the order in which Nautilus displays information as you increase the zoom level of the View pane. This tab also specifies the date format Nautilus uses.

The **List Columns** tab specifies which columns Nautilus displays, and in what order it displays them, in the View pane when you select List View.

The **Preview** tab controls when Nautilus displays or plays previews of files (Always, Local Files Only, Never).

The **Media** tab specifies which action Nautilus takes when you insert media such as a CD/DVD, or connect devices such as a flash drive, to the system.

**View** Click the **Main Toolbar**, **Side Pane**, **Location Bar**, and **Statusbar** selections in the View submenu to display or remove these elements from the window. The **Show Hidden Files** selection displays in the View pane those files with hidden filenames (page 192).

**Go** The Go selections display various folders in the View pane.

**Bookmarks** Bookmarks appear at the bottom of this menu and in the Side pane under Places. The Bookmarks selections are explained under “Places” on page 266.

**Tabs** The Tabs selections work with tabs in the Nautilus window (FEDORA).

**Help** The Help selections display local information about Nautilus.

### The Nautilus Spatial View

Nautilus gives you two ways to work with files: the traditional File Browser view described in the previous section and the innovative Spatial view shown in Figure 8-7. By default, Fedora/RHEL display the Spatial view. Other than in this section, this book describes the more traditional File Browser window. See “The Two Faces of Nautilus” on page 99 for instructions on how to turn off the Spatial view and turn on the File Browser.

The Nautilus Spatial (as in “having the nature of space”) view has many powerful features but may take some getting used to. It always provides one window per folder. By default, when you open a folder, Nautilus displays a new window.

![](img/f28adb66a7398a382f0505e0ba74a872_311_0.png)

Figure 8-7 The Nautilus Spatial view

To open a Spatial view of your home directory, double-click the Home icon on the desktop and experiment as you read this section. If you double-click the Desktop icon in the Spatial view, Nautilus opens a new window that displays the Desktop folder.

A Spatial view can display icons, a list of filenames, or a compact view. To select your preferred format, click **View** on the menubar and choose **Icons**, **List**, or **Compact**. To create files to experiment with, right-click in the window (not on an icon) to display the Nautilus context menu and select **Create Folder** or **Create Document**.

# Use **SHIFT** to close the current window as you open another window

> If you hold the **SHIFT** key down when you double-click to open a new window, Nautilus closes the current window as it opens the new one. This behavior may be more familiar and can help keep the desktop from becoming overly cluttered. If you do not want to use the keyboard, you can achieve the same result by double-clicking the middle mouse button.

**Window memory** Move the window by dragging the titlebar. The Spatial view has *window memory*—that is, the next time you open that folder, Nautilus opens it at the same size and in the same location. Even the scrollbar will be in the same position.

**Parent-folders button** The key to closing the current window and returning to the window of the parent directory is the **Parent-folders** button (Figure 8-7). Click this button to display the Parent-folders pop-up menu. Select the directory you want to open from this menu. Nautilus then displays in a Spatial view the directory you specified.

From a Spatial view, you can open a folder in a traditional view by right-clicking the folder and selecting **Browse Folder**.

![](img/f28adb66a7398a382f0505e0ba74a872_312_0.png)

**Figure 8-8** The Appearance Preferences window, Fonts tab

## GNOME Utilities

GNOME comes with numerous utilities that can make your work with the desktop easier and more productive. This section covers several tools that are integral to the use of GNOME.

### Font Preferences (FEDORA)

The Fonts tab of the Appearance Preferences window (Figure 8-8) enables you to change the font GNOME uses for applications, documents, the desktop, window titles, and terminal emulators (fixed width). To display this window, select **Main menu**: System→Preferences→Appearance or enter `gnome-appearance-properties` on a command line. Click the **Fonts** tab. Click one of the five font bars in the upper part of the window to display the Pick a Font window (discussed next).

Examine the four sample boxes in the lower part of the window and select the one in which the letters look the best. Subpixel smoothing is usually best for LCD monitors. Click **Details** to refine the font rendering further, again picking the box in each section in which the letters look the best.

### Pick a Font Window (FEDORA)

The Pick a Font window (Figure 8-9) appears when you need to choose a font; see the previous section. From this window you can select a font family, a style, and a size. A preview of your choice appears in the Preview frame in the lower part of the window. Click **OK** when you are satisfied with your choice.

### Pick A Color Window

The Pick a Color window (Figure 8-10) appears when you need to specify a color, such as when you specify a solid color for the desktop background (page 107) or a panel. To specify a color for a panel, right-click the panel to display its context menu, select Properties, click the Background tab, click the radio button labeled Solid color, and click within the box labeled Color. GNOME displays the Pick a Color window.

When the Pick a Color window opens, the bar below the color circle displays the current color. Click the desired color on the color ring, and click/drag the lightness of that color in the triangle. As you change the color, the right end of the bar below the color circle previews the color you are selecting, while the left end continues to display the current color. You can also use the eyedropper to pick up a color from the workspace: Click the eyedropper, and then click the resulting eyedropper mouse pointer on the color you want to select. The color you choose appears in the bar. Click OK when you are satisfied with the color you have specified.

![](img/f28adb66a7398a382f0505e0ba74a872_313_1.png)
