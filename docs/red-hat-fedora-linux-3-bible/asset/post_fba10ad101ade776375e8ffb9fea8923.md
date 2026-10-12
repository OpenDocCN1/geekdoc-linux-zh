
adding applications or monitors, or by changing the placement or behavior of the panel, for example.

Click any open space on either panel to see the Panel menu. The Panel menu appears as shown in Figure 3-8.

![](img/b22364e57409c2481ba806e4e6b9309c_116_0.png)

Figure 3-8: Left-click any open spot on the GNOME Panel to see the Panel menu.

From the GNOME Panel menu, you can perform a variety of functions, including:

- **Use the Applications menu** — Displayed on the Applications menu are most of the applications and system tools you will use from the desktop.
- **Add to panel** — You can add an applet, menu, launcher, drawer, or button.
- **Delete This panel** — You can delete the current panel.
- **Properties** — Change position, size, and background of the panel.
- **New panel** — You can add panels to your desktop in different styles and locations.

You can also work with items on a panel; for example you can:

- **Move items** — To move items on a panel, simply drag-and-drop them to a new position.
- **Resize items** — Some elements, such as the Window List, can be resized by clicking an edge and dragging it to the new size.
- **Use the Window List** — Tasks running on the desktop appear in the Window List area. Click a task to have that task minimized or maximized.

The following sections describe some things you can do with the GNOME panel.

## Use the Applications menu

Click Applications on the panel and you see categories of applications and system tools that you can select. Click the application you want to launch. To add an item to launch from the panel — and to view its properties — right-click it. There is currently no way to add or remove applications to or from this menu from the GUI in GNOME. However, you can manually add items to your GNOME menus.

To add to the **Applications** menu, create a *desktop* file in the `/usr/share/applications` directory. The easiest way to do that is copy an existing `.desktop` file that is on the menu you want and modify it. For example, to add a video player to the **Sound & Video** menu, you could do the following (as root user):

```bash
# cd /usr/share/applications
# cp gnome-cd.desktop vidplay.desktop
```

Next use any text editor to change the contents of the `vidplay.desktop` file you created by adding a comment, file to execute, icon to display, and application name. After you save the changes, the new item will immediately appear on the menu (no need to restart anything).

> **CROSS-REFERENCE**: There is a graphical way of modifying your Applications menu if you are using the KDE desktop. See the *Menus* bullet in the “Changing panel attributes” section later in this chapter for details.

### Adding an applet

There are several small GNOME applications, called *applets*, that you can run directly on the GNOME panel. These applets can show information you may want to see on an ongoing basis or may just provide some amusement. To see what applets are available and to add applets that you want to your panel, perform the following steps:

1.  Right-click an open space in the panel so that the panel menu appears.
2.  Select *Add to Panel*. An **Add to Panel** window appears.
3.  Select from among several dozen applets, including: a clock, dictionary lookup, stock ticker, weather report, lock screen, log out, run application, take screen shot, fortune-telling fish, eyes that follow your mouse, e-mail Inbox monitor, modem lights monitor and many others. The applet appears on the panel, ready for you to use.

Figure 3-9 shows, from left to right, geyes, system monitor, weather report, network monitor, and wanda the fish.

![](img/b22364e57409c2481ba806e4e6b9309c_117_0.png)

*Figure 3-9: Applets let you monitor activities, play CDs, watch your mail, or check the weather.*

After an applet is installed, right-click it to see what options are available. For example, select *Preferences* for the stock ticker, and you can add or delete stocks whose prices you want to monitor. If you don’t like the applet’s location, right-click it, click *Move*, slide the mouse until the applet is where you want it (even to another panel), and click to set its location.

If you no longer want an applet to appear on the panel, right-click it, and then click *Remove From Panel*. The icon representing the applet will disappear. If you find that you have run out of room on your panel, you can add a new panel to another part of the screen, as described in the next section.

### Adding another panel

You can have several panels on your GNOME desktop. You can add panels that run along the sides of the screen, to go with the ones that already go along the top and bottom. To add a panel, do the following:

1.  Right-click an open space in the panel so that the Panel menu appears.
2.  Select New Panel. A new panel appears at the right side of the screen.
3.  Right-click an open space in the new panel and select Properties.
4.  From the Panel Properties, select where you want the panel from the Orientation box (Top, Bottom, Left or Right).

After you’ve added a panel, you can add applets or application launchers to it as you did to the default panel. To remove a panel, right-click it and select Delete This Panel.

### Adding an application launcher

Icons on your panel represent a Web browser and several office productivity applications. You can add your own icons to launch applications from the panel as well. To add a new application launcher to the panel, do the following:

1.  Right-click in an open space on the panel.
2.  Select Add to Panel → Application Launcher from the menu. All application categories from your Applications menu appear.
3.  Select the arrow next to the category of application you want, select the application, and select Add. An icon representing the application appears.

To launch the application you just added, single-click it.

If the application you want to launch is not on your Applications menu, you can build one yourself as follows:

1.  Right-click in an open space on the panel.
2.  Select Add to Panel → Custom Application Launcher → Add. The Create Launcher window appears.
3.  Provide the following information for the application that you want to add:
    - **Name** — A name to identify the application (this appears in the tool tip when your mouse is over the icon).
    - **Generic Name** — A name to identify the type of application.
    - **Comment** — A comment describing the application. Like with Name, this information appears when you later move your mouse over the launcher.
    - **Command** — The command line that is run when the application is launched. You should use the full path name, plus any required options.
    - **Type** — Select Application (to launch an application). (Other selections include Link, to open a Web address in a browser or FSDevice to open a file system.)
    - **Run in Terminal** — If it is a character-based or curses application. (Applications written using the curses library run in a Terminal window but offer screen-oriented mouse and keyboard controls.)
4.  Click the Icon box (it might say No Icon). Select one of the icons shown and click **OK**. Alternatively, you can browse the file system to choose an icon.

> **NOTE:** Icons available to represent your application are contained in the `/usr/share/pixmaps` directory. These icons are either in png or xpm formats. If there isn’t an icon in the directory you want to use, create your own and assign it to the application.

5.  Click **OK**.

The application should now appear in the panel. Click it to start the application.

### Adding a drawer

By adding a drawer to your GNOME panel, you can add several applets and launchers and have them take up only one slot on the panel. You can use the drawer to show the applets and launchers as though they were being pulled out of a drawer icon on the panel.

To add a drawer to your panel, right-click the panel and then select **Add to Panel → Drawer**. The drawer should appear on the panel. The drawer behaves just like a panel. Right-click the drawer area, and add applets or launchers to it as you would to a panel. Click the drawer icon to retract the drawer.

Figure 3–10 shows a portion of a side panel that includes an open drawer. This example includes an icon for launching a Terminal window, a custom folder icon, a volume monitor, and a weather applet.

![](img/b22364e57409c2481ba806e4e6b9309c_119_0.png)

Figure 3–10: Add launchers or applets to a drawer on your GNOME panel.
