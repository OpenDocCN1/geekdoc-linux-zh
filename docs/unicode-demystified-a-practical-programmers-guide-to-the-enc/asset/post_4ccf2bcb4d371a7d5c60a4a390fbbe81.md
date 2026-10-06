
When you run who in this manner, you see a window flash on the screen for a moment and disappear. KDE ran who in a terminal emulator, who finished, and KDE closed the window. When you want to run who to run, you need to open a terminal emulator window (page 278) and give the command from the resulting window. When you call the terminal emulator in this manner, it runs a shell that persists between commands so you can see the output of. Alternatively you can give the command `bash -c 'who;read'` from the Run Command. The `-c` option causes bash to execute the string that follows the option. After it executes who, it executes read, which waits for you to enter something at the keyboard, leaving the output of who visible until you press a key.

## Cut and Paste

Two simple cut-and-paste tools are built in KDE: left mouse button/middle mouse button and CONTROL-C/CONTROL-V. For both of these techniques, you start by selecting the object (text, figure, and so on) by dragging over the object(s) you want to select. You can also double-click to select a word or triple-click to select a line. Paste the selected object by positioning the mouse pointer where you want to put the object and pressing the middle mouse button. You can give other commands after selecting the object and before you paste it, as long as you do not deselect the object.

By default CONTROL-C copies the selected text or figure, and CONTROL-V pastes the copied object at the location of the mouse pointer. You can give as many commands as you like between the CONTROL-C and the CONTROL-V, as long as you do not use another CONTROL-C. For more information, refer to “Shortcuts” on page 302. Use K menu: ApplicationsAbiAbi or K menu: Editors/Kate to experiment with these controls.

## klipper: Clipboard Utility

The clipper utility is a sophisticated multiple-buffer cut-and-paste utility. In addition to cutting and pasting from multiple buffers, clipper can execute a command on the contents of the buffer. To start clipper, choose K-menu: Run Command, enter clipper, and click Run. The clipper utility does not start a second occurrence of it when it is already running. The clipper icon (bottom of Figure 8-10) appears in the Main panel.

Each time you highlight text, clipper copies it into its buffer. The clipper icon or press ALT-CONTROL-V to display the clipper pop-up menu (Figure 8-10). The top

> 3. CONTROL-C does not copy text in a terminal emulator window because the shell running in the window intercepts the control character before KDE receives it. You must either use the mouse to cut and paste in this environment or change your shortcut/key binding (page 302).

## 284 Chapter 8 KDE Desktop Environment

![](img/aa8214d49e1cf50152c432845129fb3b_333_0.png)

Figure 8-10 klipper pop-up menu with icon

part of this menu lists the text that klipper has in its buffers. When the lines are too long to fit in the width of the window, klipper uses ellipses (...) to indicate material. To paste the text from a buffer into your document, display the klipper pop-up menu and click the line you want to; the pop-up closes. Move the mouse pointer to the location you want to paste the text and double click. In a terminal emulator window, the text is always pasted at the location of the text cursor.

## Preferences

Below the list of buffers in the klipper pop-up menu are three other choices: Actions Enabled (see the next section for a discussion of actions); Clear Clipboard History, which clears all the buffers and empties the upper part of this menu; and Preferences. When you click Preferences, klipper displays the Klipper Preferences window (Table 8-5).

## Klipper Preferences Window | Table 8-5

| General | | |
| :--- | :--- |
| Popup menu at mouse-cursor position | Specifies that when you click the klipper icon or press CONTROL-ALT-V, the klipper pop-up menu appears next to the mouse pointer. When you do not check this box, the menu appears in the lower-right corner of the workspace. |
| Save clipboard contents on exit | Specifies that klipper is to save the contents of its buffers when you quit it or close X (log out or go back to the command line prompt). |

## Klipper Preferences Window (Continued)

| | | |
| :--- | :--- |
| Replay actions on an item selected from history | Plays the appropriate action when you select a buffer from the popup menu. See "Actions," next section. |
| Prevent empty clipboard | Keeps at least the most recent item from the clipboard in the board history. |
| Timeout for Action popups | Specifies the number of seconds that the choice of actions window remains visible. Refer to "Actions," following this table. |
| Clipboard history size | Specifies the number of lines of buffers that appear on the pop-up menu. |

Refer to "Actions," following this table.

## Actions

## Shortcuts

Allows you to change three shortcuts, two of which have to do with actions. This tab works the same way as the Configure Shortcuts window, which is explained on page 302. The tab allows you to change three shortcuts: **Enable/Disable Clipboard Actions** (turns on/off the action feature of *klipper*—refer to the pop-up menu to see whether they are enabled), **Manually Invoke Action on Current Clipboard** (runs the action associated with the current buffer), and **Show Klipper Popup-Menu** (displays the pop-up menu).

## Actions

The klipper utility has the ability to execute a command when you select (fill a buffer with) that matches a specified regular expression. The regular expressions are specified under the Actions tab of the Klipper Preferences window. For example, in the Web-URL regular expression `^https?://` the description is in the column, which may not be visible until you scroll. This regular expression defines a string that begins with http, optionally followed by an s, which is followed by a colon and two forward slashes. The caret (^) matches the beginning of a line or string itself, the s? matches zero or one occurrence of s, and the two forward slashes (//) match themselves. Refer to Appendix A for more information on regular expressions.

+ 4. The Actions tab presents a portion of a wide frame, with a scrollbar at the bottom. To make your work with this frame easier, the Preferences window until the bottom scrollbar disappears. Alternatively you can scroll to the right until you see the Description heading, and drag the vertical line to the left of the word Description to make the frame narrower so that the bottom scrollbar disappears.

## Chapter 8 KDE Desktop Environment

The Action list reveals the actions that kipper can take in a tree view; click the sign in the box to the left of an action to expand the listing. Each command line has options that are appropriate to the way it is used. Under Web-URL are two lines for kmail: one to send the URL and one to send the page that the URL points to.

When you highlight a URL, such as http://www.kde.org, and press CONTROL-ALT-R kipper displays a dialog box that allows you to choose which one you want to run on the selected text. This box closes when you click a choice or for Timeout on Action pop up (see Table 8-5 on page 284), whichever occurs first.

## kipper and kmail

Many of the default actions provided with kipper send objects using kmail. These actions will not work properly unless you are running kmail at the time you give the command for kipper to take the action. You can view the error messages on the system console (typically CONTROL-ALT-F1).

## Konqueror Browser/File Manager

Even though Konqueror is much more than a Web browser, its name takes its place in the evolution of browsers: Navigator, Explorer, and now Konqueror, spelled with a K because it is part of KDE (Figure 8-11).

![](img/aa8214d49e1cf50152c432845129fb3b_335_0.png)

5. If CONTROL-ALT-R does not bring up the dialog box, try changing the Manually Invoke Action on Current Clipboard shortcut to ALT-R using the Shortcuts tab in the the kipper Preferences window.
