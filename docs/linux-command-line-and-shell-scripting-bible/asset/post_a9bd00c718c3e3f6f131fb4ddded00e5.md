
# The Linux Command Line

After the standard menu options, the View menu bar contains a list of the current active sessions. You can switch between sessions by selecting a specific session icon.

# Bookmarks

The Bookmarks menu items provide a way to manage bookmarks set in the Console window. A bookmark enables you to save your directory location in an active session and then easily return to either the same session or a new session. Have you ever drilled down several directories to find something on the Linux system, and then forgotten how you got there? Bookmarks will solve that problem. When you get to your desired directory location, add a new bookmark. When you want to return, look at the bookmarks for your new bookmark, and it'll automatically perform the directory change to the desired location for you. The bookmarks entries include:

- Add Bookmark: Create a new bookmark at the current directory location.
- Edit Bookmarks: Edit existing bookmarks.
- New Bookmark Folder: Create a new storage folder for bookmarks.

There is no limit to how many bookmarks you can store in Console, but having lots of bookmarks can get confusing. By default they all appear at the same level in the Bookmark area. You can organize them by creating new bookmark folders and moving individual bookmarks to the new folders using the Edit Bookmarks item.

# Settings

The Settings menu bar allows you to customize the appearance of a specific session. This area includes:

- Hide Menubar: Remove the menu bar from the Console window.
- Tab bar: Place the window tabs at the top or bottom of the windows, or hide them altogether.
- Scrollbar: Place the scrollbar at the right or left side of the window, or hide it altogether.
- Fullscreen: Toggle between fullscreen mode (similar to the Linux console) and as a windowed application.
- Bell: Set the action for the bell control code. This can set an audible tone, notify the Linux system, flash the Console window, or do nothing.
- Font: Set the character font, style, and size.
- Encoding: Select the character set to use in the terminal emulation.
- Keyboard: Select a keyboard mapping file to use for the session.
- Schema: Select a color schema for the background and text colors.
- Size: Set the number of columns and rows viewable in the session area.
- History: Set how much (if any) data is saved in the history scroll area.
- Save as Default: Save the current session configurations as the default.
- Save Session Profile: Save the current open sessions as a profile that you can recall later.
- Configure Notifications: Set actions for specific session events.
- Configure Shortcuts: Create keyboard shortcuts for Konsole commands.
- Configure Konsole: Create custom Konsole schemes and sessions.

Most these settings you should recognize from the discussion on terminal emulators. Konsole allows you to select character sets, keyboard layouts, and colors, and even control how the bell control is emulated within the Konsole window.

The Configure area is pretty cool. It allows you to associate five specific events that can occur within a session with six different actions. When one of the events occurs, the defined action (or actions) are taken.

The Configure Konsole settings provides for advanced control over setting session features, including creating new color schemes. Figure 2-8 shows the main Configure Konsole dialog box.

# FIGURE 2-8

The Konsole configuration dialog box

![](img/adcbcf1053b52dbf22f3aa187738232f_82_0.png)

# Part I The Linux Command Line

Within the configuration dialog box there are three tabbed areas:

- General: Allows you to set terminal emulation features such as a blinking cursor, allowing running programs to resize the terminal window using control codes, setting the line spacing, and setting the number of seconds before the session is considered inactive.
- Schema: Allows you to save a color schema for the session, and save it so that you can use it in later sessions.
- Session: Allows you to configure new and existing Konsole sessions. You can configure new sessions that start either with a standard shell or with a specific command, such as an editor.

# Help

The Help menu item provides the full Konsole handbook (if KDE handbooks were installed in your Linux distribution), a “tip of the day” feature that shows interesting-known shortcuts and tips each time you start Konsole, and the About Konsole dialog.

# The GNOME Terminal

As you would expect, the GNOME desktop project has its own terminal emulation program. The GNOME Terminal software package has many of the same features as Konsole and xterm. This section walks through the various parts of configuring and using GNOME Terminal.

# The command line parameters

The GNOME Terminal application also provides a wealth of command line parameters that allow you to control its behavior when starting it. Table 2-4 lists the parameters available.

| TABLE 2-4 | Parameter | Description |
|---|---|---|
| -e command | Execute the argument inside a default terminal window. |
| -x | Execute the entire contents of the command line after this parameter inside a default terminal window. |
| --window | Open a new window with a default terminal window. You may add multiple --window parameters to start multiple windows. |
| --window-with-profile= | Open a new window with a specified profile. You may also add this parameter multiple times to the command line. |
| --tab | Open a new tabbed terminal inside the last opened window. |
| --tab-with-profile= | Open a new tabbed terminal inside the last opened window using the specified profile. |
| --role= | Set the role for the last specified window. |
| --show-menubar | Enable the menu bar at the top of the terminal window. |
| --hide-menubar | Disable the menu bar at the top of the terminal window. |
| --full-screen= | Display the terminal window fully maximized. |
| --geometry= | Specify the X Window geometry parameter. |
| --disable-factory | Don't register with the activation nameserver. |
| --use-factory | Register with the activation nameserver. |
| --startup-id= | Set the ID for the Linux startup notification protocol. |
| -t, --title= | Set the window title for the terminal window. |
| --working-directory= | Set the default working directory for the terminal window. |
| --zoom= | Set the terminal's zoom factor. |
| --active | Set the last specified terminal tab as the active tab. |

The GNOME Command line parameters allow you to set lots of features automatically as GNOME Terminal starts. However, you can also set most of these features from within the GNOME Terminal after it starts.

# Tabs

The GNOME Terminal calls each session a *tab*, as it uses tabs to keep track of multiple sessions running within the window. Figure 2-9 shows a GNOME Terminal with three session tabs.

You can right-click in the tab window to see the tab menu. This quick menu provides a few actions for your use in the tab session:

- **Open Terminal**: Open a new GNOME Terminal window with a default tab session.
- **Open Tab**: Open a new session tab in the existing GNOME Terminal window.
- **Close Tab**: Close the current session tab.
- **Copy**: Copy highlighted text in the current session tab to the clipboard.
- **Paste**: Paste data in the clipboard into the current session tab at the current cursor location.
- **Change Profile**: Change the profile for the current session tab.
- **Edit Cursor Profile**: Edit the profile for the current session tab.
- **Show Menu**: Toggle whether the menubar is hidden or visible.

The quick menu provides easy access to commonly used actions that are available from the standard menu bar in the terminal.

# ## The menu bar

The main operation of GNOME Terminal happens in the menu bar. The menu bar contains all of the configuration and customization options you'll need to make your GNOME Terminal just the way you want. The following sections describe the different items in the menu bar.

> FIGURE 2-9

The Terminal with three active sessions

![](img/adcbcf1053b52dbf22f3aa187738232f_85_0.png)
