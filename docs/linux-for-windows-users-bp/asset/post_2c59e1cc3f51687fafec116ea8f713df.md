
## Auto-restore

When using KDE you will soon notice that it tends to start up where it left off. Any program that was left running when you logged out will probably be restored on the relevant desktop, much as you left it next time you log in. This auto-restore feature works better with some programs than with most others, as most X11-aware software will work with data that KDE cannot save. If you try to log in without saving, it will have no effect. It is a good practice to always save data before logging out, just in case it is unable to do so.

## Panel icons

There are some program icons on the Panel by default, but you can add more. To locate the relevant program files or using KFM, and this is the one, locate command structure. It is helpful in situations such as this, helpful for those who are locating files in the /opt/kde/bin folder. To place buttons on the Panel, drag the program icon from the /opt/kde/bin folder. Simply drag the applications are more or less.

![](img/147f057d2f063d8c60ee616870537a94_77_0.png)

To place icons on the Panel from KFM and onto a vacant area on the left. This will drag the program files into a vacant area on the Panel. This will leave the program, but will simply left-click on its button. The Program icons on the Panel are not used to run console applications.

The Panel icons are not used to run console applications. There is an alternate method of adding buttons to the Panel for the program in the "K" menu, which is more or less a clone of the "K" menu program structure. You find it under the "Programs" menu and select it and you add menu icons. You then select the relevant program structure. If you select the program, its button is automatically added to the Panel.

![](img/147f057d2f063d8c60ee616870537a94_77_1.png)

In order to remove a button from the Panel, right-click on the button and select Remove from the pop-up menu. (Figure 4.25). The Move option in this menu has nothing to do with moving the program file or the link to it. The button has to be moved along the Panel with the mouse. You can relocate some of the default buttons up, what is more or less detailing Properties, etc.

![](img/147f057d2f063d8c60ee616870537a94_77_2.png)

## Program icons

As pointed out in the previous chapter, you can put an icon for a program on the desktop simply by dragging it from KFM and then using the link option. This method is quick and easy. The alternative route is to give you more control over the icon. The alternative route is to do much the same way as adding a device icon to the desktop, which was described previously in this chapter. Right-click on the empty desktop and then select **New** and **Application**. This brings up a small dialogue box into which you type a suitable name for the program where it currently says **Program**. Leave the "kdeLink" part of the name unaltered. This system file extension tells the system that the file you are creating is a KDE link file.

This puts a default gearwheel icon on the desktop, but as yet it will not actually do anything. To tell the system the location of the program file, right-click on the icon and select **Properties**. On the popup menu, next click on the right link shown in Figure 4.28. If you click on the **Execute** tab to bring up the form, the path can be typed into the **Execute** edit box. Even if you do, you may prefer to use the **Browse** option.

![](img/147f057d2f063d8c60ee616870537a94_78_0.png)

Fig. 4.26 The Browse option makes it easy to find the right link

If you would like to select an alternative icon. Left-click on the gearwheel icon on this form and select a different one from the window that then opens (Figure 4.27). The gearwheel icon should then change to the one you have selected. Finally, left-click on OK to exit the **Properties** window, and then left-click on the program icon to check that it launches.

![](img/147f057d2f063d8c60ee616870537a94_78_1.png)

Fig. 4.27 Choosing an icon for the program

![](img/147f057d2f063d8c60ee616870537a94_78_2.png)

Fig. 4.28 DIY icons can be produced using the Icon Editor application

## DIY icons

If you feel like producing your own icons there is a good icon editor program available via the **K** menu. Selecting graphics and then Icon Editor will launch the Icon editor and create program (Figure 4.28).

The icons have to be quite small at only 32 pixels by 32 pixels so don't try to be too detailed. With the drawing tools down the left-hand side of the window, but with simple graphics such as icons it is often easier just to add things one pixel at a time using the paintbrush tool. To select a colour simply drag a colour from the paintbrush colour palette. Once a masterpiece is complete it should be saved to the **/opt/KDE/share/icons** folder with a ".png" extension. KDE will then be able to locate it in the Properties window where it should be included with the program icons in the standard icon. It can then be selected and used just like any other icon.

![](img/147f057d2f063d8c60ee616870537a94_79_0.png)

## KDE and RPM

As pointed out in chapter 2, these days many Linux applications are distributed in the form of RPM files. KDE includes an application called Kpackage for dealing with RPM files, and this can be activated by left-clicking on a .rpm file in KFM. In the window shown in figure 4.29 are three check boxes towards the top: 'Installed packages', 'Uninstalled packages', and 'Files to install'. This last option is the required one; when selected, left-clicking on the Install button will result in the software being installed, or error messages explaining what has gone wrong.

Kpackage is available via the "K" menu by selecting Utilities and then Kpackage. This gives a somewhat different screen (Figure 4.30), and in this form it is intended for uninstalling different RPM software. This is possible because it is a simple matter to see which of the files in the current directory is an RPM file, and when you right-click on the file, KPackage is just one of the options which comes up in your window. The first two lines located and opened which tells you the window of the RPM file as shown in Figure 4.29. The software is then installed from here in the usual way.

![](img/147f057d2f063d8c60ee616870537a94_79_1.png)

## Using Kpackage to uninstall software

When used to uninstall software, the tree at the left-hand side of the screen shows various software categories and sub-categories. Double clicking on one of these expands it to show the contents. Having located the program you wish to remove, left-clicking on it brings up details of the program on the main window area. The Uninstall button becomes active, and left-clicking on it will result in the program being removed. You will get a chance to change your mind before the uninstall procedure starts, as there is little risk of accidentally or simply uninstalling anything. If you should accidentally remove something you need to change your mind, it should be possible to locate the RPM file on the installation disc and simply reinstall it from CD-ROM using Kpackage.

## Unzip

KFM can handle zipped tar files, but it does not seem to do as well with Mac/DOS and Windows type files that have been zipped using a program such as Winzip or Pkunkzip. These files usually have ".zip" or ".arc" extensions. If you left-click on a file of this type, it will launch the Archive program, which will then display the contents of the zipped file (figure 4.31). The contents of text files can be read by clicking on the relevant file in the list, and it seems to be possible to extract some files. If extracting

![](img/147f057d2f063d8c60ee616870537a94_79_2.png)

![](img/147f057d2f063d8c60ee616870537a94_80_0.png)

Fig. 4.31 The contents of a zip file displayed by the Archiver application

files using the Archiver program proves to be impossible then it should be possible to do so via the command line and the unzip command. To use this command, just include the name of the file to be unzipped as the last part of the command, and this command will extract the files within the archive. For example, using this command would extract the files within the zip called "testfile.zip".

```
unzip testfile.zip
```

The "testfile.zip" file would have to be in the current directory, and the unzipped files would have to be placed in that directory, so there are plenty of options available with the unzip command, but for most purposes this basic form is all that is needed. Use this command if you require a list of the available options:

```
unzip --help
```

## Memory

If you limit yourself to running one application at a time it is unlikely that the amount of free memory will be a consideration unless you are trying to get by with the bare minimum. If you make a habit of running several applications at once the amount of free memory becomes more significant.

From within KDE it is possible to use one of the system information programs to get information on the amount of free memory or the way memory is allocated. Activate the K menu and then select Settings, then the System Information button in the top left of the KDE's information utility window. This opens an information window (Figure 4.32). This monitor window will continue to update its figures even when it is not the active window, so you can run various programs and note their effect on memory usage. The more programs that you run the lower the figure for "Free memory" will become.

![](img/147f057d2f063d8c60ee616870537a94_80_1.png)

Fig. 4.32 Memory information obtained from one of KDE's information utilities

![](img/147f057d2f063d8c60ee616870537a94_80_2.png)

Fig. 4.33 Memory information obtained via the command line

It is also possible to obtain some facts and figures about memory usage from the command line interpreter. The most basic command line utility for monitoring memory is the free command, and to use it you simply type in this command:

```
free
```

This provides much the same information as its KDE equivalent, including a figure for the amount of free memory (Figure 4.33). There are other system monitoring programs available via the "K" menu and the Settings - Information route, including information about the free
