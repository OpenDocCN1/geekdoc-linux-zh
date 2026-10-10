
In mid-2002, version 2.0 of GNOME was released. This version uses new internal data structures, and doesn’t coexist well with earlier versions of GNOME. Thus, you shouldn’t try to mix and match GNOME 2.0 or later components with programs from earlier versions of GNOME.

Figure 23-2 shows a GNOME environment. Compared to the one shown in Figure 23-1, you can see that GNOME is quite similar to KDE, at least on a first pass. Both environments include control bars (called the Panel in both environments) from which you can launch programs, switch between programs, or switch between virtual desktops. Like KDE, GNOME ships with a tool called the Control Center (the front-most window in Figure 23-2), which you can use to configure GNOME features. Both environments support desktop icons for launching programs, opening documents, and so on.

GNOME differs from KDE in many details. GNOME’s window manager is more readily configured than is KDE’s. (Figure 23-2, and most screen shots in this book, use IceWM and its Helix theme.) Because GNOME is built from GTK+, KDE is built atop Qt, buttons, menu, and so on look different in the two environments. Individual components such as calculators and editors have different feature mixes. The default GNOME configuration provides a Panel at the bottom of the screen and a menu bar at the top, with some functionality duplicated in both places.

If you want to decide between GNOME and KDE, your best course of action may be to try each environment for a week or two. Which environment works best for you is largely a matter of personal preference based upon the many small differences between the two.

## Xfce

Compared to KDE and GNOME, Xfce is a small desktop environment, both in terms of its absolute size and in terms of its popularity. Like GNOME, Xfce is built upon GTK+. GNOME and KDE both take inspiration from GUI desktop environments on non-UNIX platforms, such as Windows, OS/2, and Mac OS Classic. Xfce, by contrast, draws heavily from the commercial UNIX CDE package. Features of Xfce include:

- **Window manager** Xfce uses its own window manager, XFwm. This window manager isn't as configurable as some others, but it is functional.
- **File manager** Xfce provides a file manager called XFiler. Like many other Xfce components, XFiler isn't as flashy as its KDE or GNOME counterparts, but it's quite usable.
- **Desktop tools** Xfce provides several desktop tools. Some of these, such as the desktop panel (equivalent to the GNOME or KDE Panel) are Xfce-specific. Others, such as the calculator, are unaffiliated but common X programs that Xfce is configured to run.

Xfce doesn't include any office suite tools, although you can run GNOME Office, KOffice, or other office tools from the program. Likewise, Xfce doesn't ship with an Xfce-centric web browser, but it does come configured to run Mozilla once installed. Xfce ships with substantially less in the way of GUI configuration and support tools than either KDE or GNOME, and many of Xfce's tools are less flashy than equivalents in other environments. (Figure 23-3 shows an Xfce desktop.) If you find Xfce adequate for your needs, its small size can be a great boon, particularly on a low-memory computer.

## Rolling Your Own Desktop Environment

One of the strengths of X is that its modular nature enables users to customize their desktops to a degree that's not possible with many other GUI environments. If you try KDE, GNOME, and Xfce, and discover that you don't like these environments, even with the customizations they offer, you can reject all of them and start from scratch. This task, although probably not the best choice for a newcomer to X, is not as difficult as it would be on some OSs. You don't have to be able to write any programs to create your own desktop environment; you need only mix and match the components you want.

![](img/f34d37e3abe9f4517128e54f80ab2616_593_0.png)

**Figure 23-3.** *XFce provides fewer features in its configuration and desktop management tools than KDE or GNOME, but it’s a less resource-hungry environment.*

You should begin your quest with a window manager. FreeBSD includes many options in the x11-wm packages or ports area. Good options for a lightweight environment include IceWM, WindowMaker, fvwm and its variants, Sawfish, and Black Box. People who want the most configurable and flashy window manager should investigate Enlightenment.

A bare window manager may be all you need if you want a truly austere GUI environment. If not, you can add components by launching them from the same configuration file you use to launch the window manager itself, as described in Chapter 6 and the upcoming section, “Starting GNOME.” You can run a file manager from KDE, GNOME, or Xfce. Independent file manager projects also exist, such as Desktop File Manager (DFM; http://www.kaiservice.de/dfm/), Gento (http://www.obsession.se/gento/), and TKDesk (http://tkdesk.sourceforge.net). In fact, the x11-fm ports and packages section is devoted to examples of this class of program.

After collecting a window manager and file manager, the task of developing your own desktop environment becomes one of locating all the little support programs you might want to help make you productive—calculators, e-mail clients, editors, and so on. Many of these tools ship with FreeBSD, so finding them isn't difficult if you take some time to browse the available packages using sysinstall. Making them available from your custom desktop environment usually involves editing a window manager or file manager configuration file. As a general rule, window managers use configuration files named after themselves in your home directory, or subdirectories with several configuration files. For instance, IceWM uses `~/icewm/preferences` for overall preferences and `~/icewm/menu` for items on its menu. You can edit the latter file to add programs to the IceWM menu. File managers use similar configuration files. For instance, DFM uses the `~/.dfmnext` file to associate file types to programs, so that you can launch a program by double-clicking a data file associated with the program. The `~/.dfmdesk` directory contains files associated with icons that appear on the desktop. You can use DFM's own context menus to add a program to the desktop, and that action creates a link or file in the `~/.dfmdesk` directory.

Some tools provided by integrated desktop environment packages, such as programs to set the mouse tracking speed, are best handled in a roll-your-own environment by much simpler tools that you run from your startup script. For instance, you can use `xset` to set X features such as your mouse tracking speed and keyboard repeat rate, and `xsetroot` to set the background color. You might include lines like the following in your `.xinitrc` or `.xsession` file to adjust these values:

```
xset m 4
xset r 250 15
xsetroot -solid SteelBlue
```

The first of these lines sets the mouse acceleration to a value of 4 (the precise effect of this command varies from one mouse and display to another). The second line sets the keyboard to auto-repeat when you hold down a key, beginning 250 milliseconds after the keypress begins, with 15 repeats per second thereafter. The third line sets the desktop background color to blue. Consult the `xset` and `xsetroot` man pages for more information on what these commands can do.

The main advantage to creating your own desktop environment is that you'll get something that's closer to what you want than might be possible with a prepackaged desktop environment, particularly on a low-memory system. KDE and GNOME offer many features, but they might not *exactly* match what you want, and they come at a large price in memory use. Creating your own environment may help you use a system that's low on resources.

## Using GNOME

GNOME is a popular FreeBSD desktop environment. It's also very similar to KDE in its overall feature set and operation, although many details differ. This section describes

![](img/f34d37e3abe9f4517128e54f80ab2616_594_0.png)
