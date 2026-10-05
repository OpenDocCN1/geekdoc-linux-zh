
# CHAPTER 4 INTRODUCTION TO UBUNTU LINUX

occupies the whole workspace; click the same button (now displaying a square in place of the up arrow) on the title of a maximized window to restore the window to its former size. You can also double-click the title to maximize and restore your window. Clicking the close button closes the window and usually terminates the program running in. To reposition the window, left-click the title and drag the window to the desired location.

## Window Operations

The Window Operations menu contains operations that you most commonly need to perform on your window. Right-click either the titlebar or the Window List applet (page 121) to display this menu. You can use this menu to move a window to another workspace, keep the window on top of or below others windows, and keep the window to always be visible on the displayed workspace.

## Toolbar

A toolbar (Figure 4-16, preceding page) usually appears near the top of a window and contains icons, text, applets, menus, and more. Many kinds of toolbars exist. The titlebar is not a toolbar; rather, it is part of the window decorations placed by the window manager (page 155).

## CHANGING THE INPUT FOCUS (WINDOW CYCLING)

The window with input focus is the one that receives keyboard characters and commands you type. In addition to using the Window List applet (page 121), you can change which window on the displayed workspace has the input focus by the keyboard; this process is called window cycling. When you press ALT-TAB, GNOME displays in the center of the workspace a box that holds icons representing the programs running in the workspace. It also shifts the input focus to the window that was active just before the current active window, making it easy to switch back and forth between two windows. When you hold ALT and press TAB multiple times, the focus moves from window to window. Holding ALT and SHIFT and repeatedly pressing TAB cycles in the other direction. See page 153 for more information on the input focus.

## CUTTING AND PASTING OBJECTS USING THE CLIPBOARD

There are two ways to cut/copy and paste objects on the desktop and both within windows. In the first method, you use the clipboard, technically called the copy buffer, to copy or move objects or text. To do so, you explicitly copy an object or text to the buffer and then paste it somewhere. Applications that follow the user interface guidelines use CONTROL-X to copy, CONTROL-C to copy, and CONTROL-V to paste. Context menus frequently provide these options.

You may not be familiar with the second method to copy and paste text—using the selection or primary buffer, which always contains the text you most recently selected (highlighted). You cannot use this method for copy objects. Clicking the middle mouse button (click the scroll wheel on a mouse that has one) pastes the contents of the selection buffer at the location of the mouse pointer. If you are using a two-button mouse, click both buttons at the same time to simulate clicking the middle button.

With both these techniques, start by highlighting an object or text to select it. You can drag a box around multiple objects to select them or drag the mouse pointer over text to select it. Double-click to select a word or triple-click to select a line or a paragraph.

Next, to use the clipboard, explicitly copy (CONTROL-C) or cut (CONTROL-X) the objects or text. If you want to use the selection buffer, skip this step.

To paste the selected objects or text, position the mouse pointer where you want to put it and then press CONTROL-V (clipboard method) or press the middle mouse button (selection buffer method).

### Use SHIFT-CONTROL-C AND SHIFT-CONTROL-V within a terminal emulator

- tip: The CONTROL-C, CONTROL-X, and CONTROL characters do not work in a terminal emulator window because the shell running in the window intercepts them—the terminal emulator can receive them. You can use SHIFT-CONTROL-C and SHIFT-CONTROL-X, respectively, in their place. There is no keyboard shortcut for CONTROL-X. You can also use the selection buffer in this environment or use copy/paste from the Edit selection on the menubar or from the context menu (right-click).

When using the clipboard, you can give as many commands as you like between CONTROL-C or CONTROL-X and CONTROL-V, as long as you do not press CONTROL-C or CONTROL-X again. When using the selection buffer, you can give other commands after selecting (highlight) and before pasting it, as long as you do not select text.

## GETTING THE MOST OUT OF THE DESKTOP

The root window is any part of a workspace that is not occupied by a window, panel, or object. It is the part of the workspace where you can see the background. To view the window when it is obscured, click the Desktop button at the left end of the panel to minimize the windows in the workspace.

Desktop menu Right-click the root window to display the Desktop menu, which enables you to create a folder, launcher, or document. Change Desktop Background opens the Preferences window (page 113).

## RUNNING COMMANDS FROM A TERMINAL EMULATOR/SHELL

A terminal emulator is a window that presents a command-line interface (CLI); it functions as a textual (character-based) terminal and is displayed in a graphical environment. To display the GNOME terminal emulator named Terminal (Figure 4-18), select Main menu: Applications -> Terminal or enter the command gnome-terminal. Because you are already logged in and creating a subshell in a desktop environment, you do not need to log in again. Once you have opened terminal emulator window, try giving the command man to read about (page 136), which displays manuals. Chapter 5 describes utilities you can run from a terminal emulator. You can also start graphical programs, such as eyes, from within the window.

When you are in a terminal emulator window, several characters, *, ], have special meanings. Avoid using these characters until you have read "Special Characters" on page 160.

## THE OBJECT CONTEXT MENU

When you right-click an object or group of objects on the desktop or in a File Browser window, GNOME displays an Object context menu. Different types of objects display different context menus, but most context menus share common selections. Figure 4-19 shows context menus for an OpenOffice.org spreadsheet and a plain text file. Table 4 lists some Object context menus.

| Open with OpenOffice.org Spreadsheet | Open with gedit |
|---|---|
| Open with Archive Manager | Open with OpenOffice.org Word Processor |
| Open with Archive Mounter | Open with Other Application... |
| Open with Other Application... | Cut |
| | Copy |
| | Make Link |
| | Rename... |
| Copy to | Copy to |
| Move to | Move to |
| Move to Trash | Move to Trash |
| Stretch icon... | Stretch icon... |
| Restore Icon Original Size | Restore Icon Original Size |
| Extract Header | Compress... |
| Send To... | Send To... |
| Properties | Properties |

**Figure 4-19** The Object context menus for a spreadsheet (left) and a text file (right)

## Table 4-1 Object context menu selections

- Open: Runs an executable file. Opens a file with an appropriate application. Opens a folder in a File Browser window. Same as double-clicking the object.
- Open in New Window: (From a File Browser window only.) Opens a folder in a new File Browser window instead of replacing the contents of the current window. Same as holding down shift while double-clicking a folder in a File Browser window.
- Open with '*App': Opens the file using the application name App. When this selection appears as the first selection in the menu, App is the default application GNOME uses to open this type of file.. See page 130 for information on changing this default.
- Open with ➤: A triangle appearing to the right of a selection indicates a menu. Allow the mouse pointer to hover over the selection to display the submenu. Each submenu selection is an Open with '*App*' selection (above). The last selection in the submenu is Open with Other Application (below).
- Browse Folder: (On the desktop only.) Opens a folder in a File Browser window. Same as double-clicking a folder on the desktop.
- Open with Other Application: Displays the With menu, which allows you to select an application for this type of file. The next time you use the Object context menu to open this file, the application you selected as an Open with '*App*' selection (above). Does not change the default application for this type of file. See page 130 for information on changing the default application.
- Cut: Removes the object and places it on the clipboard (page 124).
- Copy: Copies the object to the clipboard (page 124).
