
> **NOTE**
>
> You may not have the Konsole terminal emulation package installed on your system. If you would like to install it, see Chapter 9, “Installing Software,” to learn how to install software via the command line.

Click the Konsole icon with your mouse to open the terminal emulator. An open Konsole application on an Ubuntu distribution is shown in [Figure 2-10](#).

![](img/a5025f22e05b92f409563a958cac7312_75_0.png)

**FIGURE 2-10** The Konsole terminal emulator

Remember that, in most desktop environments, you can create a keyboard shortcut to access applications such as Konsole. The command you need to type for the shortcut in order to start up the Konsole terminal emulator is **konsole**. Also, if the Konsole application is installed, you can start it from another terminal emulator by typing **konsole** and pressing Enter.

> **TIP**
>
> In the Plasma desktop environment, the Konsole terminal emulator application already has a default keyboard shortcut: Ctrl+Alt+T.

The Konsole terminal emulator, similar to GNOME Terminal, has several configuration options provided by menus and shortcut keys. The following section describes these various features.

## The menu bar

The Konsole menu bar contains the configuration and customization options you need to easily view and change features in your terminal emulation session. The following tables briefly describe the menu options and associated shortcut keys.

> **TIP**
>
> If the Konsole menu bar is not currently displayed, you can press Ctrl+Shift+M to enable it.

The File menu, shown in *Table 2-10*, provides options for starting a new tab in the current window or in a new window.

### TABLE 2-10 The File Menu

| Name | Shortcut Key | Description |
| :--- | :--- | :--- |
| New Window | Ctrl+Shift+N | Starts a new shell session in a new Konsole Terminal window |
| New Tab | Ctrl+Shift+T | Starts a new shell session in a new tab in the existing Konsole Terminal window |
| Clone Tab | None | Starts a new shell session in a new tab in the existing Konsole Terminal window that attempts to duplicate the current tab |
| Save Output As | Ctrl+Shift+S | Saves the current tab's output in its scrollback buffer as either a text or an HTML file |
| Print Screen | Ctrl+Shift+P | Prints the current tab's displayed text |
| Open File Manager | None | Opens the default file browser application |
| Close Session | Ctrl+Shift+W | Closes the current tab session |
| Close Window | Ctrl+Shift+Q | Closes the current Konsole window |

Notice that Konsole offers two handy options for saving information from your shell session: Save Output As and Print Screen. The Print Screen function allows you to print the displayed text to a system printer or save it as a PDF file.

> **NOTE**
>
> As you read through these Konsole menu options, keep in mind that your Linux distribution's Konsole application may have very different menu options available. This is because some Linux distributions have kept older versions of the Konsole terminal emulation package.

The Edit menu, shown in Table 2-11, provides options for handling text in the session. Also, managing tab names is in this options list.

### TABLE 2-11 The Edit Menu

| Name | Shortcut Key | Description |
| :--- | :--- | :--- |
| Copy | Ctrl+Shift+C | Copies selected text to the Konsole clipboard |
| Paste | Ctrl+Shift+V | Pastes text from the Konsole clipboard into a session |
| Select All | None | Selects all the text in the current tab |
| Copy Input To | None | Starts/stops session input copies to chosen additional sessions |
| Send Signal | None | Sends the selected signal from the drop-down menu to the current tab's shell process or other process |
| Rename Tab | Ctrl+Alt+S | Modifies session tab title bar setting |
| ZModem Upload | Ctrl+Alt+U | Starts the process of uploading a selected file, if the ZMODEM file transfer protocol is supported |
| Find | Ctrl+Shift+F | Opens the Find window to provide scrollback buffer text search options |
| Find Next | F3 | Finds the next text match in more recent scrollback buffer history |
| Find Previous | Shift+F3 | Finds the next text match in older scrollback buffer history |

Konsole provides an excellent method for tracking what function is taking place in each tab session. Using the Rename Tab option, you can name a tab to match its current task. This helps in tracking which open tab session is performing what job.

> **NOTE**
>
> **Konsole retains a history, formally called a *scrollback buffer*, for each tab. The history contains output text that** has scrolled out of the terminal viewing area. By default, the last 1,000 lines in the scrollback buffer are retained. You can scroll back through the scrollback buffer by simply using the scrollbar in the viewing area. Also, you can scroll back line by line by pressing the Shift+Up Arrow or scroll back a page (24 lines) at a time by pressing Shift+Page Up.

The View menu, shown in Table 2-12, contains items for controlling individual session views in the Konsole Terminal window. In addition, options are available that aid in monitoring terminal session activity.

### TABLE 2-12 The View Menu

| Name | Shortcut Key | Description |
| :--- | :--- | :--- |
| Split View | None | Controls a multiple tab session display within the current Konsole window |
| Detach Current Tab | Ctrl+Shift+L | Removes a tab session and starts a new Konsole window using this tab session |
| Detach Current View | Ctrl+Shift+H | Removes the current tab session's view and starts a new Konsole window with it |
| Monitor for Silence | Ctrl+Shift+I | Toggles on/off a special message when no activity is occurring in the tab session |
| Monitor for Activity | Ctrl+Shift+A | Toggles on/off a special message when activity starts occurring in the tab session |
| Read-only | None | Toggles on/off the terminal session accepting keyboard strokes; does *not* enable/disable keyboard shortcuts |
| Enlarge Font | Ctrl++ | Enlarges the font size in the window incrementally |
| Reset Font Size | Ctrl+Alt+0 | Returns the font size to default |
| Shrink Font | Ctrl+- | Reduces the font size in the window incrementally |
| Set Encoding | None | Selects the character set used to send and display characters |
| Clear Scrollback | None | Removes the text in the current session's scrollback buffer |
| Clear Scrollback and Reset | Ctrl+Shift+K | Removes the text in the current session's scrollback buffer and resets the terminal window |
| Full Screen Mode | F11 | Toggles on/off the terminal window filling the entire monitor display area |

The Monitor for Silence option is used for indicating tab silence. Tab silence occurs when no new text appears in the current tab session for about seven seconds. This allows you to switch to another tab while waiting for the application's output to stop.

> **TIP**
>
> The Konsole application provides a simple menu when you right-click in the active session area. Several menu items are available in this easy-to-access menu.

The Bookmarks menu options, shown in Table 2-13, provide a way to manage bookmarks set in the Konsole window. A bookmark enables you to save your active session's directory location and then easily return there in either the same session or a new session.

### TABLE 2-13 The Bookmarks Menu

| Name | Shortcut Key | Description |
| :--- | :--- | :--- |
| Add Bookmark | Ctrl+Shift+B | Creates a new bookmark at the current directory location |
| Bookmark Tabs | None | Creates a new bookmark for all current terminal tab sessions |
| New Bookmark Folder | None | Creates a new bookmark storage folder |
| Edit Bookmarks | None | Edits existing bookmarks |

The Settings menu, shown in Table 2-14, allows you to customize and manage your profiles. Profiles allow a user to automate the running of commands, set up the session's appearance, configure the scrollback buffer, and so on. Also, within the Settings menu you can add a little more functionality to your shell sessions.

### TABLE 2-14 The Settings Menu

| Name | Shortcut | Key Description |
| :--- | :--- | :--- |
| Edit Current Profile | None | Opens the Edit Profile window to provide profile configuration options |
| Switch Profile | None | Applies to the current tab a selected profile |
| Manage Profiles | None | Opens the Manage Profiles window to provide profile management options |
| Show Menubar | Ctrl+Shift+M | Toggles on/off menu bar display |
| Configure Keyboard Shortcuts | None | Creates Konsole command keyboard shortcuts |
| Configure Notifications | None | Creates custom Konsole notifications |
| Configure Konsole | Ctrl+Shift+, | Configures many Konsole features |

Configure Notifications allows you to associate specific events that can occur within a session with different actions, such as playing a sound. When one of the events occurs, the defined action (or actions) is taken.

The Help menu, shown in Table 2-15, provides the full Konsole handbook (if KDE handbooks were installed in your Linux
