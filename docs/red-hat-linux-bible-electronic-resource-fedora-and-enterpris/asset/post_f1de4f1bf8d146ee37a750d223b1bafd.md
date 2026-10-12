
## Adding a launcher to the panel

1. Right-click in an open space on the panel.
2. Select Add to Panel → Launcher. The Create Launcher window appears.
3. Provide the following information for the application that you want to add:
   - **Name** — A name to identify the application (this appears in the tool tip when your mouse is over the icon).
   - **Generic Name** — A name to identify the type of application.
   - **Comment** — A comment describing the application. Like with Name, this information appears when you later move your mouse over the launcher.
   - **Command** — The command line that is run when the application is launched. You should use the full path name, plus any required options.
   - **Type** — Select Application (to launch an application). (Other selections include Link, to open a Web address in a browser, or FSDevice to open a file system.)
   - **Run in Terminal** — If it is a character-based or curses application. (Applications written using the curses library run in a Terminal window but offer screen-oriented mouse and keyboard controls.)
4. Click the Icon box (it may say No Icon). Select one of the icons shown and click OK. Alternatively, you can browse the Red Hat Linux file system to choose an icon.

> **NOTE:** Icons available to represent your application are contained in the `/usr/share/pixmaps` directory. These icons are either in png or xpm formats. If there isn't an icon in the directory you want to use, create your own and assign it to the application.

5. Click OK.

The application should now appear in the panel. Click it to start the application.

## Adding a drawer

By adding a drawer to your GNOME panel, you can add several applets and launchers and have them take up only one slot on your panel. You can use the drawer to show the applets and launchers as though they were being pulled out of a drawer icon on the panel.

To add a drawer to your panel, right-click the panel and then select Add to Panel → Drawer. The drawer should appear on the panel. The drawer behaves just like a panel. Right-click the drawer area, and add applets or launchers to it as you would to a panel. Click the drawer icon to retract the drawer.

Figure 3-10 shows a portion of the panel that includes an open drawer. This example includes icons for launching a Terminal window, the GIMP, and the Ethereal window.

![](img/27a85d56d393921ced6412ae6e8336bf_119_0.png)

## Changing panel properties

Properties you can change that relate to a panel are limited to the position, size, hiding policy, and background. To open the Panel properties window that applies to a specific panel, right-click on an open space on the panel, then choose Properties. The Panel properties window that appears includes the following values:

- **Panel Type** — You can see whether the panel is an Edge, Aligned, Sliding, or Floating panel (you can't change this value).
- **Position** — Depending on the type of panel, you can move it to different locations on the screen by clicking on a new position.
- **Size** — You can select the size of your panel, from XX Small (12 pixels) to XX Large (128 pixels).
- **Autohide** — You can select whether or not a panel is automatically hidden (appearing only when the mouse pointer is in the area).
- **Show hide buttons** — You can choose whether or not the Hide/Unhide buttons (with pixmap arrows on them) appear on the edges of the panel.
- **Arrows on hide buttons** — If you select "Show hide buttons" you can select to either have arrows on those buttons or not.
- **Background** — From the Background tab, you can assign a color to the background of the panel, assign a pixmap image, or just leave the Default (sort of gray). Click the Background Type box, if you want to select an Image for the background, then select an image, such as a tile from `/usr/share/backgrounds/tiles` or other directory.

> **TIP:** I usually turn on the AutoHide feature and turn off the Hide buttons. Using AutoHide gives you more space to work with on your desktop. When you move your mouse to the edge where the panel is, it pops up — so you don't need Hide buttons.

## Using the Nautilus file manager

At one time, file managers did little more than let you run applications, create data files, and open folders. These days, as the information a user needs expands beyond the local system, file managers are expected to also display Web pages, access FTP sites, and play multimedia content. The Nautilus file manager, which is the default GNOME file manager, is an example of just such a file manager.

When you open the Nautilus file manager window (from the GNOME main menu or by opening the Home icon or other folder on your desktop), you see the name of the location you are viewing (such as the folder name) and what that location contains (files, folders, and applications). Figure 3-11 is an example of the file manager window displaying the home directory of a user named chris (/home/chris).

![](img/27a85d56d393921ced6412ae6e8336bf_120_0.png)

Figure 3-11: Move around the file system, open directories, launch applications, and open Samba folders.

Icons on the toolbar of the Nautilus window let you move forward and back among the directories and Web sites you visit. To move up the directory structure, click the up arrow. To refresh the view of the folder or Web page, click the Refresh button. The Home button takes you to your home page and the Web search button lets you search the Web.

> **NOTE:** One note about viewing HTML content (in other words, Web pages). The version of Nautilus that originally came with GNOME 2.4 did not properly display HTML content. Depending on how the fix for this problem falls out, HTML content may not be displayed in the Nautilus window. Instead, you might have the option of launching an external window (such as Mozilla or Epiphany) to display that content.

Icons in Nautilus often indicate the type of data that a particular file contains. The contents or file extension of each file can determine which application is used to work with the file. Or, you can right-click an icon to open the file it represents with a particular application or viewer.

Some of the more interesting features of Nautilus are described below:

### Sidebar

Click on View → Side Pane to have a sidebar appear in the left column of the screen. From the sidebar, you can click on tabs that represent different types of information you can select. The Tree tab shows a tree view of the directory structure, so you can easily traverse your directories.

The Notes tab lets you add notes that become associated with the current Directory or Web page. The History tab displays a history of directories and Web sites you have visited, allowing you to click those items to return to the sites they represent. Right-click in the sidebar to choose which of the sidebar tabs are displayed.

### Windows File and Printer Sharing

If your computer is connected to a LAN on which Windows computers are sharing files and printers, you can view those resources from Nautilus. Type **smb:** in the location box to see available workgroups. Click a workgroup to see computers from that workgroup that are sharing files and printers. Figure 3-12 shows an example of Nautilus displaying icons representing Windows computers in a workgroup called estreet (smb://estreet).

![](img/27a85d56d393921ced6412ae6e8336bf_121_0.png)

### MIME types and file types

To handle different types of content that may be encountered in the Nautilus window, you can set applications to respond based on MIME type and file type. With a folder being displayed, right-click a file for which you want to assign an application. Click either Open With an Application or Open With a Viewer. If no application or viewer has been assigned for the file type, click Associate Application to be able to select an application. From the Add File Types window, you can add an application based on the file extension and MIME type representing the file.
