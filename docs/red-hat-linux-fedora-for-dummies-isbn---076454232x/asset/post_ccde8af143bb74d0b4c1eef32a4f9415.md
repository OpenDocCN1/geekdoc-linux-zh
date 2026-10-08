
## Exploring the GNOME Desktop

GNOME performs all the basic graphical functions you expect from a desktop environment. You can set the background and create icons, for example. This section shows how to perform some basic GNOME desktop maneuvers and configurations. After you master the basics, you can continue to explore on your own.

The default GNOME desktop — as installed by the Red Hat Linux installation — comes with several elements preinstalled. Let's take a quick trip around the desktop.

### Introducing the default desktop icons

In the upper-left corner of the desktop are three icons: your home directory, Start Here, and Trash (refer to Figure 9-1). They perform these tasks:

![](img/8c094d1b36276212c03d10d898508a6e_138_0.png)

**Home directory:** This icon, which looks like a folder, represents your home directory. For example, if you create a user account named `lidia`, a directory named `/home/lidia` is created; the icon is labeled `lidia’s Home`. When you log in as `lidia`, the home directory icon is linked to that directory. Double-click the home directory (or right-click and choose Open) and a Nautilus window opens, displaying the contents of the home directory.

Double-clicking an icon opens the window associated with the icon. For example, double-clicking your home directory opens a Nautilus file manager window linked to your home directory. You can also open an icon by right-clicking it and choosing the Open option.

**Start Here:** GNOME provides a Preferences window that includes links to the major GNOME and Red Hat configuration utilities and applications. Double-click the Start Here icon and the Start Here window opens. Opening any of the icons — Applications, Preferences, Server Settings, or System Settings, for example — opens another Nautilus window that provides access to utilities and applications:

- **Applications icon:** Clicking the Applications icon is equivalent to clicking the GNOME Menu. You see a window of icons that mirrors the GNOME Menu. Any item you can reach from the GNOME Menu, you can access from the Applications icon.
- **Preferences:** Clicking the Desktop Properties icon is equivalent to choosing GNOME Menu > Preferences. You get to choose from a number of GNOME configuration options. The GNOME Preferences window is described later in this chapter, in the “Making GNOME Recognize MIME Types” section.
- **System Settings:** Double-clicking the System Settings icon opens the System Settings window, which allows you to start various administrative utilities. You find icons, such as Red Hat Network Configuration, and the Printing utilities here.
- **Trash icon:** GNOME provides a method to dispose of files and directories in the form of the Trash directory. Click any icon, file, or directory and drag it to the Trash icon. Although Jesse James' Monster Garage automated trash minivan doesn’t come for your file, it’s placed in the Trash directory; the Trash directory is in your home directory.

Trashed items aren’t really deleted until you right-click the Trash icon and choose Empty trash. You can undelete items by opening the Trash (double-clicking the icon) and then clicking the item and dragging it out onto the desktop or an open Preferences window.

![](img/8c094d1b36276212c03d10d898508a6e_138_1.png)

### Changing themes and backgrounds

GNOME provides the ability to change the look and feel of its elements. The look and feel of an element — typically, a window opened on the desktop — is referred to as its *theme*. *Themes* determine the size, shape, texture, and color of the buttons, slides, menus, borders, and other pieces of an open window.

You can change your theme more easily and quickly than a politician during an election by choosing GNOME Menu > Preferences > Theme; alternatively, you can open the *Start Here* icon and select *Preferences* in the window that opens. Double-click the *Theme* icon when the *Preferences* window opens.

When the *Theme Preferences* window opens, the *Application* tab is activated by default. You can select any theme and all your open windows immediately adopt it. The application theme changes the tint and texture applied to each window. For example, clicking the *Metal* theme gives your windows a brushed surface appearance.

Click the *Window Border* tab. Click any of the themes and your window borders change. Window borders consist of the tint and texture of the strip that surrounds each window and the buttons on the strip.

Keep selecting different themes until you find one you like. Click the *Close* button when you’re finished.

You can also select the image that’s displayed on your desktop. The image can be a picture, a pattern, or solid colors. Change the desktop to find one you like by right-clicking any blank (uncluttered) section of the desktop.

Choose Change Desktop Background from the menu and the Background Preferences window opens. Select an image by clicking the Picture section or one of its variations. The Please Select an Image window opens. You can select any listed image or search for another image on your disk. Alternatively, you can select a solid color by clicking the No Picture button.

Open the Background Style menu and select either a solid color or colors that change on the vertical or horizontal axis. You can then change the color (solid or gradient) by clicking the Color button. Select your color from the Pick a Color window. Repeat the process for the other color, and you get a screen full of colors.

Right-clicking anywhere on a blank section of the desktop and then choosing Use Default Background resets the background. The default background gets reactivated.

### Toiling in your workplace

After using GNOME for a while, you find that as you start more and more applications, you create lots and lots of windows on the screen. You may even lose windows behind other windows. Perhaps you want to strap together several monitors so that you can display all the windows at one time.

Monitors are expensive and bulky, so you're probably stuck using a single monitor. But you don't have to stick with one *screen*. GNOME lets you spread your work across multiple *virtual monitors*.

Imagine that you have a large GNOME desktop spread equally across four monitors. Life would be good if you could open windows on any of the monitors. You would have lots of real estate to spread out on.

However, because you probably don't have four monitors, GNOME simulates four *virtual monitors*, called *workspaces*. Each workspace is equivalent to a real monitor, and you can spread out your work across it. The only limitation is that you can view only one workspace at a time.

### Trading places on your workspace switcher

Switching between workspaces is easy. GNOME provides a utility, the Workspace Switcher, to select any workspace. The Workspace Switcher is on the GNOME Panel.

You use the GNOME Workspace Switcher to access each workspace. The Workspace Switcher is divided into four quadrants. Clicking any of the quadrants places you in the corresponding desktop. Click the lower-right one and you enter that workspace.

You can force a window into any or all workspaces. Click the downward-facing arrow in the upper-left corner of a window. The menu that opens provides all the expected functions that close, minimize, maximize, and resize the window. However, toward the bottom of the menu are options for placing the window in any of the remaining three workspaces; or, you can put the window in all the workspaces. You may want, for example, to put an application like Mozilla in all workspaces in order to use it no matter what you're doing.

### Messing Around with Windows

Before you can do anything to a window, you have to get its attention. When you have a window's attention, it has *focus*. Depending on how you have set up GNOME, you can give a window focus with GNOME in several ways:

- Click the window's name on the GNOME Panel.
- Click the window's title bar, at the top of the window.
- Click a part of the window itself, which typically also makes the window the topmost one. This method is the default.
- If you're working in an office with lots of people, you can shout, "Hey, you — wake up!" Although this tactic isn't likely to wake up your window, it sure is fun.

![](img/8c094d1b36276212c03d10d898508a6e_141_0.png)

In this book, we stick with the Red Hat and GNOME default of clicking a window to give it focus.

### Moving windows

To move a window, click anywhere on the window's title bar and hold down the left mouse button. As long as you continue to hold down that button, the window moves anywhere you move your mouse. Release the button and the window stays there.

### Resizing windows

Sometimes, a window is a little too big or a little too small, and you know that life would be much easier if you could just nudge that window into shape. To
