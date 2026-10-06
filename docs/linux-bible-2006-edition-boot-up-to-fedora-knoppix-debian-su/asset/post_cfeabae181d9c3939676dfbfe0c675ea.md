
## Configuring the Desktop

If you want to change the look, feel, or behavior of your KDE desktop, the best place to start is the KDE Control Center. The Control Center window (see Figure 3-6) lets you configure dozens of attributes associated with colors, fonts, backgrounds, and screen savers. You can also change attributes relating to how you work with windows and files.

To open the KDE Control Center from the desktop, select Control Center from the K menu or use a Terminal window and type sudo kcontrol.

![](img/a2d958d7eab32ca5b89b2b8af808aa70_128_0.png)

Click the plus (+) sign next to the topic you want to configure, and select the particular item you want to configure. The following sections describe some of the features you can configure from the Control Center.

## Changing the Display

You can change a lot of the look-and-feel of your desktop display. Under the Appearance & Themes topic (click the plus sign), you can change Background, Colors, Fonts, Icons, Launch Feedback, Panel, Screen Saver, Style, Theme Manager, and Window Decoration.

Here are a few of the desktop features you may want to change:

- **Background**—Under the Appearance & Themes heading in the KDE Control Center, by default, all of your virtual desktops use the same background. To have different backgrounds for each virtual desktop, select the next box to the Setting for Desktop heading, choose any of the four desktops, and then choose the background you want for the current desktop.
For each desktop, select Picture, Slideshow, or No Picture. For a Picture, there are several backgrounds you can choose from the pull-down menu, or you can browse your file system for a picture. To do a slide show, click Slideshow and select Setup (to choose your pictures and define how they change).
Click Apply to your selections.

- **Screen Saver**—Under the Appearance & Themes heading, select Screen Saver. From the window that appears, select from a list of screen savers. KNOPPIX includes only a blank screen saver. Fedora Core comes with about 160 different screen savers. If you prefer Slideshow, you can have a slide show of images for your screen. Click Setup to identify an image directory or modify the screen saver. Under settings, select how many minutes of inactivity before the screen saver turns on. You can also choose Require Password to require before the screen saver starts. If you have any virtual terminals open, switch to them and use `vlock` to lock each of them as well. (You need to install the vlock package if it isn't available.)

![](img/a2d958d7eab32ca5b89b2b8af808aa70_129_0.png)

If you are working in a place where you want your desktop to be secure, be sure to turn on the Password feature. This prevents others from gaining access to your computer when you forget to lock or shut it off. If you have any virtual terminals open, switch to them and use `vlock` to lock each of them as well.

- **Fonts**—You can assign different fonts to different places in which fonts appears on the desktop. Under the Appearance & Themes heading, select one of the categories of fonts (General, Fixed width, Toolbar, Menu, Window, Taskbar, and Desktop fonts). Then click the Choose box to select a font from the Select list box that you want to assign to that category. If the font is available, an example of the text appears in the Sample text box.

![](img/a2d958d7eab32ca5b89b2b8af808aa70_129_1.png)

To use 100 dpi fonts, you need to add an extra for 100 dpi fonts to `/etc/xorg.conf` file. If you make that change, you need to restart the X server for it to take effect.

Other attributes you can change the selected size (in points) and character set (to select an ISO character set). Select Apply to apply the changes.

- **Colors**—Under the Appearance & Themes heading, select Colors. The window appears lets you change the color of items on the desktop. Select a whole color scheme from the Color Scheme list box or select an item from the Widget color box to change a particular item. Items you can change text, backgrounds, links, buttons, and title bars.

## Changing Panel Attributes

For most people, the panel is the place where they select which desktop is active and which applications are run. You can change panel behavior from the Configure window. Right-click any empty space on the panel, and then select Configure Panel. You can change these features from the Settings window that appears:

- **Arrangement**—Change the location of the panel by clicking Top, Left, or Right in the Panel list box. The Panel selection style lets you change the size of the panel from Medium to Tiny, Small, or Large.
- **Hiding**—Certain selections enable you to authorise the panel or use hide buttons. Under the Hide Mode heading, choose whether to hide only when a panel hiding button is clicked or to hide automatically after a set number of seconds when the cursor is not in the panel area. You can also show or not hiding buttons. Sliders let you select the delay and speed at which panels and buttons appear.
- **Menus**—Unlike the GNOME main menu, with KDE you have the capability to manipulate the main menu from the GUI. Click the Edit K menu. The KDE editor allows you to cut, copy, paste, and modify submenus and applications from your main menu.

## Adding Launchers and MIME Types

You want be able to quickly access the applications that you use most often. One of the best ways to make that possible is to add icons to the panel or the desktop that can launch the applications you need with a single click. Procedures for adding applications to the panel and desktop are described in the following sections.

## Adding Applications to the Panel

You can add any KDE application to the KDE panel quite easily. Here's how:

- Right-click an open space on the panel.
- Choose Add+ Application.
- Select one of the categories of applications.
- Select any application from that category (or select Add This Menu to add the whole menu of applications).

An icon representing the application immediately appears on the panel. (If the seems a bit crowded, you might want to remove some applications you don't.)

If you decide later that you no longer want this application to be available on the panel, right-click the edge of the icon and click the Remove button. Move it to a different location on the panel, right-click it, click Move, move it to where you want it on the panel, and click again.

## Adding Applications to the Desktop

To add an application to the desktop, use the desktop menu. Here's how:

1. Right-click an open area ⬘ Link to Application from the menu.
2. Select Create Core in the Properties window that appears, click the General tab and replace Link to Application with the name you want to appear for the application on the desktop. On that same tab, click the gear icon and select one icon from the list to represent your application.
3. Click the Application tab and add a description of the application and comment. Then in the Command box, type the command you want to run or browse your file system (click the Browse button) to find the command to run.
4. Click OK, and the icon for the new application launcher appears on the desktop.

If you decide that you no longer want this application to be available on the desktop, right-click the icon and click Delete or Move to Trash.

## The GNOME Desktop

GNOME (pronounced guh-name) provides the desktop environment that you get by default when you install Fedora Core and other Red Hat Linux systems. This desktop environment provides the software that is between your X System framework and the look-and-feel provided by the window manager. GNOME is a stable and reliable desktop environment, with a few cool features.

The new GNOME 2.10 desktop comes with the most recent version of Fedora Core. For GNOME 2.10, enhancements include a new volume manager (for managing removable media), keyring manager (for managing keys), and remote desktop preferences. To use your GNOME desktop, you should become familiar with the following components:

- **Metacity (window manager)** — The default window manager for GNOME in Fedora and RHEL is Metacity. Metacity configuration options let you control the things you see, and window borders and controls used on your desktop.
- **Nautilus (file manager/graphical shell)** — When you open a folder (by clicking the Home icon on your desktop, for example), the Nautilus window opens displays the contents of the selected folder. Nautilus can also display other types of content, such as shared folders from Windows computers on the network (using SMB).
- **GNOME panels (application/task launcher)** — These panels, which line the top and bottom of your screen, are designed to make it convenient for you to launch the applications you use, manage running applications, and work with multiple desktops. By default, the top panel contains menu buttons (Applications, Places and Desktop), desktop application launchers (Evolution
