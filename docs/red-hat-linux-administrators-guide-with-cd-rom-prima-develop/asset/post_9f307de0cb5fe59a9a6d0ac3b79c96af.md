
The script automatically starts the easiest installation method for your system. You can choose which packages you want to install. After you make your selections, the script fetches the packages from the Internet and installs them automatically. This is the reason that you need a root console.

However, it should be mentioned that a cracker could theoretically exploit this script. My recommendation is to download the packages to your drive and verify their authenticity before running the command to upgrade or install the packages.

If you wish to run the install script yourself, the steps are nearly the same:

- Download the file `installer-latest-intel.gz` from the helixcode.com homepage and place it in a temporary directory. This directory can be one of your making in your home directory or a unique directory in /tmp. Keep the files separate from others.
- Unzip the file by entering `gunzip installer-latest-intel.gz`.
- Make the file executable by entering `chmod u+x installer-latest-intel`.
- Now run the installer by entering `./installer-latest-intel`.

After making sure that you have a viable Internet connection, the installer program begins connecting to the respective Helix GNOME site. The program tests your system for the latest software and then lets you choose the packages to install.

Once the most current Helix GNOME files are loaded, you will have an auto-loader function so that you can later upgrade to newer releases. The temporary directory stores the downloaded files until they are installed; afterward they are deleted. You may copy these files to a separate directory for use elsewhere or for selected upgrades on machines not connected to the network. However, because of the library dependencies, it is best to save all the files and install them at once.

Helix GNOME has a much cleaner interface than the standard GNOME desktop. It also provides several additional utilities that do not normally come with GNOME, including extra window managers such as the new Sawfish (formerly Sawmill) program. Helix GNOME demonstrates just how dynamic the Linux platform is becoming.

# Discussing the Features of KDE

KDE is currently considered by some to be the forerunner in the quest for easy-to-use Linux interfaces. Although it has not been that long since the Linux community split between the two camps of GNOME and KDE, they have since resolved many of their differences and now are cooperating in their separate developments in order to appeal to both sets of users. The GNOME developers took the open-source stance, stating that only GNOME conformed to the higher standards required by the GPL. Meanwhile the KDE project managers and enthusiasts pointed to the stability of KDE and its user-friendly interface. They also held the position that KDE was quickly becoming accepted by many in the Linux community despite the stipulations of the Qt license. But as the Qt developers saw the wisdom in making their source code free and open, both camps of thought have reached an understanding. Recently the Qt developers have decided to release the Qt libraries under the GPL, thus removing any limitations that purist Linux enthusiasts may have had concerning its use.

According to the developers of KDE, their project is not just a window manager, though it does technically use a manager for its interface. Rather, KDE is considered by its makers to be a *desktop environment*, which is reflected in its name, the *K Desktop Environment* (KDE).

KDE relies upon many applications built with the Qt libraries. That does not limit it, however, from running programs based on non-Qt libraries. Netscape and GIMP, which are built with a different set of libraries, can still be run under KDE. The external appearance and framework match that of the KDE window build, whereas the internal buttons and links still use their own libraries and retain their own appearance. KDE and the KDE window manager (kwm) look alike because they both are built on the Qt libraries. GNOME and its window manager may not necessarily both use GTK and thus can appear different. Window Maker, for example, which does not depend on GTK, can be run jointly with the GNOME panel.

KDE's appearance is very much a hybrid combination of the Windows and Macintosh desktops (see Figure 12.2). The K Application Starter button on the lower panel, which provides a complete listing of the KDE utilities, is reminiscent of Windows. Yet some of the other icons resemble the Macintosh OS. With KDE Themes, you can make the desktop seem even more like its proprietary counterparts or give it an entirely different look, one truly unique in its own right.

The lines and framework of the windows are clean and defined. Though it may appear at first glance to operate like Windows, there are distinct differences. First, a panel appears at the bottom of the screen, which like a Windows panel can be positioned elsewhere on the page and resized. However, the upper portion of the screen features a taskbar that displays currently running programs, similar to an Apple utility. By clicking the large “K” icon on the lower left, much like to the Start button under Windows, you can see the various types of programs that run under KDE. It too is fully configurable; you can add additional Start buttons to the panel to create your own set of icons and preset programs. You can also minimize this entire panel to either side or corner of the desktop and place the running programs in a drop-down menu located on the top of the screen. This configuration provides yet more space on the desktop and still keeps visible the programs running under the GUI.

![](img/a0884097af3186d9b4f616aaa3f065b0_436_0.png)

# FIGURE 12.2

A vanilla KDE install, displaying its basic features and window appearance.

KDE also provides information about the other virtual desktops used under KDE. For example, you can run an application on one virtual desktop and then switch to a different virtual desktop, where you can run another, unrelated program. This clears up much of the clutter associated with the limitations of having just one screen in which to accomplish all the tasks. Nor do all the programs clutter up the panel. Each program, when minimized, is associated with its own virtual desktop. Switching to another virtual desktop provides a new pristine space to store running programs.

A vanilla KDE configuration provides just four default virtual desktops, each with its own window number as a name. Under older window managers, these windows were called *pagers*, which you could use to bring up or page a new workspace. Clicking on each panel’s respective link brings up the new virtual desktop. KDE can hold as many as eight virtual desktops, each of which you can rename with a specific identity.

When using KDE, I like to identify each desktop with a specific task. One virtual desktop is titled “Internet,” and holds all the Internet-related programs, such as the browser, links to URLs, and so on. Another is termed “Mail” and holds all mail clients. Yet another is called “Network” and has open terminal windows to other machines on the internal network or LAN. Such a naming scheme helps in organizing a desktop. No longer must you hunt through the various minimized icons for the running application. Simply switching to the correctly named virtual desktop will provide all associated programs in its category. Nearly all window managers provide this type of functionality.

## Theming the Desktop

As is the case with nearly all window managers, KDE allows you to customize the desktop appearance to whatever size, shape, or color you wish. KDE also encourages those more adventurous to tweak the source code to advanced levels of customization. For those who lack the knowledge to undertake such tweaking, or who simply like the general design, KDE offers different *themes* or visual patterns for users to use to configure the appearance even more. A theme allows users to change the default window borders, fonts, background, and icons to a more customized appearance.

Some themes are based on other operating systems or television shows and movies. Figure 12.3 shows another example, a theme called DrawingBoard. The basic premise is to relate all the graphics to a specific subject matter. For example, a theme might set a particular tone by using a distinct background image such as cartoon characters and then having the other images reflect the same feel
