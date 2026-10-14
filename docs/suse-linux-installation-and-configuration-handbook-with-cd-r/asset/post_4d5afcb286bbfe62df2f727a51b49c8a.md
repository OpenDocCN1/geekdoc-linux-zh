
- **shell Patterns**—Check this option to easily select and deselect files using the shell patterns and wild cards.
- **Auto save setup**—If this option is set, Midnight Commander will save its current settings when you exit it. Then, the next time you start Midnight Commander, it will use the last setting you left it on.
- **auto menus**—If set, when you start Midnight Commander the user menu will immediately pop up.
- **use internal edit**—This option controls the default editor invoked when the F4 key is pressed over a file. If you do not want Midnight Commander to use its internal editor, uncheck this option and export the EDITOR environment variable to your preferred editor. For example, the default editor could be set to nedit:
  `export EDITOR=nedit.`
- **use internal view**—If you want to setup Midnight Commander to use its internal viewer, you can do so by checking this option. If you want to declare an external viewer to be used by Midnight Commander, you can do so by deselecting this option and exporting the PAGER environment variable to your desired viewer.
- **Complete: show all**—This option is important for users who use the mini command line provided by Midnight Commander. When set, Midnight Commander will show all the available completion patterns possible for your search if you press the Alt+Tab keys.
- **rotating dash**—When enabled, Midnight Commander will show a rotating dash in the corner of the screen to represent activity when running a command.
- **FynX-like motion**—This option makes directory navigation easier by enabling you to use the left/right arrow keys to enter and exit directories.
- **advanced chown**—When enabled, the Advanced chown dialog will be invoked if you use the chown or chmod commands.
- **cd follows links**—If this option is enabled, Midnight Commander follows the logical chain of directories. If you uncheck this option, Midnight Commander follows the real directory structure. It is recommended that you set this option so you will return to your original directory when you enter a link; otherwise, you will be taken to the parent directory of the link instead of the directory that contains the link.
- **safe delete**—If enabled, the delete confirmation dialog will require you to type in your confirmation on the delete operation. This is different from the Yes/No dialog that is set up in Layout Options.

## The Layout Dialog

You can change the layout of Midnight Commander using the Layout dialog (see Figure 31.3). You can access this dialog through Options, Layout.

In the Layout dialog, you can specify how the file view should be split in the Panel split group. You can specify whether you want the split to be vertical or horizontal by selecting one of the radio buttons in the options box. You also can set up the width and height of each panel. If you decide they should be equally split, you can select the Equal split check box.

In the Highlight section, you can select to highlight the file permissions or file types. It is recommended that you check both boxes.

In the Other options group box, you can specify other layout options such as the following:

- **menubar visible**—Using this option, you can set the menubar on top of Midnight Commander to always be visible.
- **show mini status**—If you check this box, when you move the selection bar over a file, the file information you selected to show in the right/left menus will be shown in a bar called mini status.
- **command prompt**—If this check box is checked, Midnight Commander will show a one-line mini command prompt that you can use to enter shell commands. To view the output of this command, press the Ctrl+O combination.
- **Keybar visible**—This option shows a list of buttons at the bottom of the screen with the important shortcut command. The buttons are Norton Commander-style buttons. This option is recommended if you are going to use the mouse with Midnight Commander. It also is recommended for novice Midnight Commander users.
- **hintbar visible**—Midnight Commander shows a random hint under the file list view. If you want to disable this hintbar to gain more display space, you can disable this option.
- **Xterm hintbar**—If you open Midnight Commander using terminal emulator in X Windows, the window title bar will show the Midnight Commander hints. This option is great for saving display space and showing Midnight Commander hints at the same time.

### FIGURE 31.3

Using the Layout menu, you can control the look and feel of Midnight Commander.

![](img/659f91d9da7b29976c0625e2e9628511_634_0.png)

## The Confirmation Dialog

Midnight Commander can be configured to verify a specific command. Suppose that you pressed F8, which deletes a file, by mistake. Following the better-safe-than-sorry philosophy, Midnight Commander gives you the ability to confirm such critical commands. You can reach the Confirmation dialog by Options, Confirmation. The following are its options:

- Confirm delete—Check this box to ensure you don't delete a directory or file by mistake.
- Confirm overwrite—Check this box to ensure you do not overwrite a file by mistake.
- Confirm execute—If you want Midnight Commander to confirm before it runs an executable file, check this box.
- Confirm exit—If checked, Midnight Commander will ask for a confirmation if you press F10. It will not ask for confirmation if you issue the exit command on the command line.

## Display Bits

Midnight Commander runs on a wide range of UNIX-compatible operating systems. The display bits on each of these systems vary. SuSE Linux is capable of using Full 8 bits output. You should check this box along with the Full 8 bits input. This option is very important if you are going to use Midnight Commander with programs such as acon, which can be used to edit and view Arabic language text within Midnight Commander.

## Learn Keys

On many systems, the terminal keys do not work. Fortunately, with SuSE Linux, you will not have to worry about broken terminal keys. On the other hand, some terminal emulation programs under X Windows might be broken. To ensure that you correct the settings for those terminal emulation programs, start the Learn Keys dialog from the Options, Learn Keys menu and enter your keyboard mapping.

## Virtual Filesystem Settings

Midnight Commander uses a virtual filesystem of its own to store information it needs to configure to make navigation local and remote directories faster for the user. You can tweak the settings for the Midnight Commander virtual filesystem using the Options, Virtual File System Setting menu (see Figure 31.4). The dialog contains the following options:

### FIGURE 31.4

Using the Virtual File System Setting menu, you can set up the preferences that determine how Midnight Commander should treat caching.

![](img/659f91d9da7b29976c0625e2e9628511_635_0.png)

Timeout for freeing VFSs—This is the timeout in seconds after which Midnight Commander will forget the cached information it has about local directory listings or a compressed file's contents.

FTP anonymous password—When logging in as an anonymous user on FTP, you can change the password to be anything you enter in this field. You should make sure that the entry in this field is a valid email address. Some FTP sites require the password to be in a valid email address format even if the email address does not exist.

ftpfs directory cache timeout—This is the timeout in seconds after which Midnight Commander will forget the cached information it has about a remote directory listing on an FTP.

Always use FTP proxy—If you check this box, you must enter the gateway of the proxy server in the gateway field. Midnight Commander will use the proxy server settings when requesting remote files.

## Saving the Settings

After you have set up the layout configuration for Midnight Commander, you should save your settings by choosing the Options, Save Setup menu item. If you do not save your settings, you will have to reconfigure Midnight Commander the next time you start it.
