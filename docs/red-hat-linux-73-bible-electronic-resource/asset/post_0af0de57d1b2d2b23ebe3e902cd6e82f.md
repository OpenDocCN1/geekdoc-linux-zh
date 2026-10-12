
- **Show hide buttons** — You can choose whether or not the Hide/Unhide buttons (with pixmap arrows on them) appear on the edges of the panel.
- **Background** — From the Background tab, you can assign a color to the background of the panel, assign a pixmap image, or just leave the standard background (sort of gray). Click the Background Type box, and then select the pixmap (from the /usr/share/pixmaps or other directory) or color to assign to the panel.

> TIP: I usually turn on the AutoHide feature and turn off the Hide buttons. Using AutoHide gives you more space to work with on your desktop. When you move your mouse to the edge where the panel is, it pops up—obviating any need for the Hide buttons.

## Using the Nautilus file manager

At one time, file managers did little more than let you run applications, create data files, and open folders. These days, as the information a user needs expands beyond the local system, file managers are expected to also display Web pages, access FTP sites, and play multimedia content. The Nautilus file manager, which is the default GNOME file manager, is an example of just such a file manager.

When you open the Nautilus file-manager window (from the GNOME main menu or by opening the Home icon on your desktop), you will see a sidebar in the left-hand column and the files and directories contained in the current directory in the right-hand column. Figure 4-3 is an example of the file-manager window displaying the home directory of a user named jake (/home/jake).

![](img/1744bde8c889adfab3fc911e1687fecf_155_0.png)

Figure 4-3: Move around the file system, open directories, launch applications, and browse the Web from Nautilus.

Icons on the toolbar of the Nautilus window let you move forward and back among the directories and Web sites you visit. To move up the directory structure, click the up arrow. To refresh the view of the folder or Web page, click the Refresh button. The Home button takes you to your home page and the Web search button lets you search the Web.

Many data files are represented by icons that indicate the type of data they contain. The contents or file extension of each file can determine which application is used to work with the file. Or, you can right-click an icon to open the file it represents with a particular application or viewer.

Some of the more interesting features of Nautilus are described below:

- **Sidebar** — The left column of the screen consists of a sidebar. From the sidebar, you can click on tabs that represent different types of information you can select. The Tree tab shows a tree view of the directory structure, so you can easily traverse your directories. The News tab lets you select from a variety of news sites and has headlines displayed from those sites.
- The Notes tab lets you add notes that become associated with the current Directory or Web page. The Help tab opens links to the GNOME Help system. The History tab displays a history of directories and Web sites you have visited, allowing you to click those items to return to the sites they represent.
- **Web browsing** — By typing a Web address (URL) in the Location box on the Nautilus window or by clicking on a link, Nautilus acts as a Web browser by displaying the requested content. Select Web search to have your favorite search engine displayed to search for Web sites (www.google.com is used by default).
- **MIME types and file types** — To handle different types of content that may be encountered in the Nautilus window, you can set applications to respond based on MIME type and file type. With a directory being displayed, click a file for which you want to assign an application. Click either Open With an Application or Open With a Viewer. If no application or viewer has been assigned for the file type, click OK to be able to select an application. From the File Types and Programs window, you can add an application based on the file extension and MIME type representing the file.

> **CROSS-REFERENCE**: For more information in MIME types, see the description of MIME types in the “Changing GNOME preferences” section later in this chapter.

- **Drag-and-Drop** — You can use drag-and-drop within the Nautilus window, between the Nautilus and the desktop, or between multiple Nautilus windows. As other GNOME-compliant applications become available, they are expected to also support the GNOME drag-and-drop feature.

If you need more information on the Nautilus file manager, visit the Eazel Web site at http://nautilus.eazel.com. Eventually, support for Nautilus will move to the GNOME Web site (www.gnome.org/nautilus).

## Changing GNOME preferences

There are many ways to change the behavior, look, and feel of your GNOME desktop. Some of these relate directly to GNOME, whereas others must be changed for the window manager (in this case, sawfish). Most GNOME preferences can be modified in the Control Center window. You can open that window from a Terminal window as follows:

```
# gnomecc &
```

The Control Center window contains categories for changing preferences related to the Desktop, Document Handlers (editors, MIME types, and URLs), the current window manager, and other features. The following sections describe the preferences that you can change.

## Changing the desktop

From the Control Center window, you can change the Background, Launch Feedback, Panel, Screensaver, Theme Selector, or Window Manager for your GNOME desktop. After you open the Control Center window, select one of those categories. Here are the preferences that you can change from each:

- **Background** — From the Background preferences, you can choose a single solid color, a two-color gradient (shading from top to bottom or left to right), or a pixmap image to use as wallpaper. If you choose a single solid color, click the color box under Primary Color, choose a color from the palette, and select OK. To have the color fade into another color, click Vertical or Horizontal Gradient, and then select the second color. Choosing Vertical has the colors transform from top to bottom, while Horizontal causes the colors to change from left to right.

To use wallpaper for your background, click Browse. You can choose from a variety of images in the /usr/share/nautilus directory. Then, choose to have the image tiled, centered, scaled (in proportion), or scaled (using any proportion to fill the screen).

- **Launch Feedback** — From the Launch Feedback preferences, you can indicate the kind of behavior the GNOME exhibits while an application is being launched. While an application is being launched from the desktop, you can enable feedback in a tasklist, have an hourglass appear for the mouse cursor, have a splash screen displayed while the application launches, or have an animated star displayed.

- **Panel** — From the Panel section, you can change global behavior of the panels on your desktop. These selections are described earlier in the Using the GNOME Panel section.

- **Screensaver** — You can choose dozens of screensavers from the Screen Saver preferences window. Select Random Screensaver to have your screen saver chosen randomly, or select one that you like from the list. Next, choose how long your screen must be idle before the screen saver starts (default is 20 minutes). You can also choose to require a password or to enable power management to shut down your monitor after a set number of minutes.

### Finding Desktop Themes

New desktop themes for GNOME/sawfish are available from the sawfish.themes.org Web site. To select and download a Sawfish desktop theme, do the following:

1. Make sure that the Sawfish themes directory is available for downloading the themes. You can use either of the following two directories:
   `/usr/share/sawfish/themes` or `$HOME/.sawfish/themes`.
   Use the first directory if you want any user on your Red Hat Linux system to be able to use the theme. Use the second directory if you want the theme available only for your own use.
2. Go to the following Web site: `http://sawfish.themes.org`.
   (To search for themes other than the ones listed on the main Sawfish themes page, use the search box at the top of the page.)
3. Click any theme that looks interesting from those available at `sawfish.themes.org`.
4. On the page that appears describing the theme, select the **Download** link. You will be prompted again to download the theme.
5. Click **Download**. You are asked to select a location to which to download the file.
6. Type the path to either of the Sawfish themes directories noted in Step 1. The theme file is downloaded to that directory. (You can close the browser for the moment.)
7. Go to the Sawfish themes directory and unzip the file. For example, to unzip a theme called `Whatever.tar.gz`, you would type the following from a Terminal window: `cd /usr/share/sawfish/themes` and then `tar xvfg Whatever.tar.gz`.

At this point, the desktop theme is ready to be used.

- **Theme Selector** — You can choose to have an entire theme of elements be used on your desktop. A desktop theme affects not only the background, but also the way that many buttons and menu selections appear. There are about a dozen themes available with the Red Hat Linux distribution. See the sidebar “Finding Desktop Themes” for information on how to get additional desktop themes.
