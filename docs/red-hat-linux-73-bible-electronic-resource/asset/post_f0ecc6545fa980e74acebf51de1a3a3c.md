
- **Cascade windows** — Right-click the desktop, and then click Cascade windows on the menu. The windows are aligned as they are with the Uncluttered selection, except that the windows are each indented.
- **Rolling up windows** — Double-click the title bar of a window to roll it up like a window shade. Double-click the title bar again to roll the window down again. This is a great way to clear a window away for a time, without fully minimizing it.

## Moving windows

The easiest way to move a window from one location to another is to place the pointer on the window’s title bar, move the mouse so the window goes to a new location, and release the mouse button to drop the window. Another way to do it is to click the window menu button (top left corner of the title bar), click Move, move the mouse to relocate the window, and then click again to place it.

If somehow the window gets stuck in a location where the title bar is off the screen, there is a way you can move it back to where you want it. Hold down the Alt key and press the left mouse button in the inner window. Then move the window where you want it and release.

## Resizing windows

To resize a window, place the pointer over a corner or side of the window border, then move it until it is the size you want. Grabbing a corner lets you resize vertically and horizontally at the same time. Grabbing the side lets you resize in only one direction.

You can also resize a window from the window menu button. Click the window menu button (top left corner of the title bar) and select Size. Move the mouse until the window is resized and click to leave it there.

## Using virtual desktops

To give you more space to run applications than will fit comfortably on your physical screen, KDE gives you access to several virtual desktops at the same time. Using the 1, 2, 3, and 4 buttons on the Panel, you can easily move between the different desktops. Just click the one you want.

If you want to move an application from one desktop to another, you can do so from the window menu. Click the window menu button for the window you want to move, click To Desktop, then select Desktop 1, 2, 3, or 4. The window will disappear from the current desktop and move to the one you selected.

## Using sticky windows

When you are using multiple virtual desktops (the 1, 2, 3, or 4 on the Panel), there are times when you want the same window to appear on every one of them. For example, you may want a clock to appear in the upper corner of all desktops or a stock ticker to run along the bottom of all desktops.

To stick the window, click the pushpin icon so it appears to be pressed in. To unstick a window, use the same control. Click the pushpin again.

Any application that you always want available is a candidate for sticking. Some good examples are xclock (to always view a clock), xconsole (to see system messages), xeyes (so eyes can watch your every move), and xbiff (to have an indicator show you when mail arrives).

## Configuring the desktop

If you want to change the look, feel, or behavior of your KDE desktop, the best place to start is the KDE Control Center. The KDE Control Center window lets you configure dozens of attributes associated with colors, fonts, backgrounds, and screen savers used by KDE. You can also change attributes relating how you work with windows and files.

To open the KDE Control Center from the desktop, either click the KDE Control Center icon on the Panel or click the K button → Control Center. The KDE Control Center window appears, as shown in Figure 4-7.

![](img/1744bde8c889adfab3fc911e1687fecf_174_0.png)

Figure 4-7: Configure your desktop from the KDE Control Center.

Click the plus (+) sign next to topics you want to configure. Then select the particular item you want to configure. The following sections describe some of the features you can configure from the KDE Control Center.

## Changing the display

There are several ways you can change the look and feel of your desktop display. Under the Look & Feel topic (click the plus sign), you can change Background, Colors, Desktop, Fonts, Icons, Launch Feedback, Panel, Screensaver, Shortcuts, Style, Taskbar, Theme Manager, Window Behavior, and Window Decoration.

Here are a few of the desktop features you may want to change:

- **Change the background** — Under the Look & Feel heading in the KDE Control Center, select Background. You can remove the “X” next to Common Backgrounds to choose to have a common background for all four of your virtual desktops or assign backgrounds to individual desktops.

First select the Mode: Flat (single color); Pattern (two colors and click Setup to select a pattern); Background Program (click Setup to choose a program to run on the background); Horizontal Gradient (two colors that fade from left to right); Vertical Gradient (two colors that fade from top to bottom); Pyramid Gradient (two colors that fade from outside in); Pipecross Gradient (two colors that fade from the outside to a cross in the middle); and Elliptic Gradient (two colors that fade from outside to an ellipse in the middle).

If you prefer to use a wallpaper on the background, click the Wallpaper tab and select a desktop. Choose a Mode (to indicate the position of the wallpaper) and click the Wallpaper box to scroll down to choose the wallpaper. If you have a JPEG image you would like to use instead, click the Browse button to select the image you want from your file system. Click the Multiple box if you want to assign several wallpapers that change at set intervals.

Click Apply to apply your selections.

- **Change the screensaver** — Under the Look & Feel heading, select Screensaver. From the window that appears, select from about 25 different screen savers. Click Setup to modify the behavior of the screen saver. Under settings, select how many minutes of inactivity before the screen saver turns on. You can also click **Require password** to require that a password be entered before you can access your display after the screen saver has come on.

> **TIP:** If you are working in a place where you want your desktop to be secure, be sure to turn on the **Require Password** feature. This prevents others from gaining access to your computer when you forget to lock it or shut it off. If you have any virtual terminals open, switch to them and type `vlock` to lock each of them as well. (You need to install the vlock package if the `vlock` command isn't available.)

- **Change fonts** — You can assign different fonts to different places in which fonts appear on the desktop. Under the Look & Feel heading, select Fonts. Select one of the categories of fonts (General, Fixed width, File manager, Toolbar, Menu, Window title, and Taskbar fonts). Then click the Choose box to select a font from the Select Font box that you want to assign to that category. If the font is available, you will see an example of the text in the Sample text box.

> **TIP:** If you want to use 100 dpi fonts, you need to add an entry for 100 dpi fonts to the `/etc/XF86Config` file. After you make that change, you need to restart the X server for it to take effect.

Other attributes you can change for the selected fonts are size (in points) and character set (to select an ISO standard character set). Select Apply to apply the changes.

- **Change the colors** — Under the Look & Feel heading in the KDE Control Center, select Colors. The window that appears lets you change the color of selected items on the desktop. Select a whole color scheme from the Color Scheme box. Or select an item from the Widget color box to change a particular item. Items you can change include text, backgrounds, links, buttons, and title bars.

## Changing panel attributes

For most people, the Panel is the place where they select which desktop is active and which applications are run. You can change some of the behavior of the panel from the KDE Control Center. (Select Panel under the Look & Feel heading.) Here are the features you can change from each of the tabs:

- **Position** — Change the location of the panel by clicking on Top, Left, Bottom, or Right in the Panel Location box. The Panel Style selection lets you change the size of the Panel from Medium to Tiny, Small, or Large.

- **Hiding** — There are selections that allow you to autohide the panel and hide buttons. Under the Hide Buttons heading, choose whether or not hide buttons are put on each outside edge (left/top or right/bottom) of the Panel. Sliders let you select the delay and speed at which panels and buttons are hidden.

- **Look & Feel** — You can enable icon zooming (so icons bulge out as the mouse passes over them), have tool tips appear, and enable background tiles. You can select a background image for the Panel. You can also assign different tile colors for different types of applications you add to the Panel.

- **Menus** — Choose options associated with menus. You can clear the menu cache after a set number of seconds or select to show hidden files on browser menus. For the K Menu, you can select to merge different menu locations, show the recent documents submenu, and show the quick browser submenu. By defining a Quick Start section, you can have the most recently or most frequently used items accessible from that menu.

## Adding application launchers and MIME types

You want to be able to quickly access the applications that you use most often. One of the best ways to make that possible is to add icons to the panel or the desktop that can launch the applications you need with a single click. Procedures for adding applications to the panel and desktop are described in the following sections.
