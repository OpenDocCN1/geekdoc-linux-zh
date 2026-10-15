
You can experiment to see which printer selection works best for your printer if its model is not listed. You might not be able to use all the features of your printer, but you will be able to set up printer service. Click Next when you have made your choice.

Now you can name the printer and give it a description and location as shown in Figure 8.4. The name is important, as this will be what the users see when they print. The description and location are optional, but Ubuntu autofills your location with the hostname of your computer.

![](img/8f9e74e2b343ff525bebfb720a3d8441_221_0.png)

**FIGURE 8.4** Give your printer a meaningful name, and if you want, a description and location.

If you are happy with the details, click the Apply button to commit your changes to the system.

You can see the new printer defined in the system-config-printer main window as shown in Figure 8.5.

## Editing Printer Settings

You also use the system-config-printer tool to edit the newly defined printers. To edit the printer settings, highlight the printer’s listing in the printer browser window. You can then select specific settings related to that printer by using the tabs that appear in the right side of the dialog box. The Settings dialog is shown in Figure 8.6.

The first tab in this dialog enables you to assign a new name for the printer. In this example, the printer has the name Officejet. Other tabs in this dialog enable you to change the queue type or queue options (such as whether to print a banner page or set

the image area of a page), to select or update the driver, or to choose available print options for the printer (shown in Figure 8.7).

![](img/8f9e74e2b343ff525bebfb720a3d8441_222_0.png)

**FIGURE 8.5** New printer entries displayed in `system-config-printer`'s main window.

![](img/8f9e74e2b343ff525bebfb720a3d8441_222_1.png)

**FIGURE 8.6** Edit a printer’s settings by using tabs in `system-config-printer`.

![](img/8f9e74e2b343ff525bebfb720a3d8441_223_0.png)

FIGURE 8.7 A printer's policy options can be changed on the Policies tab of system-config-printer.

When you finish editing your printer click the Apply button to save your changes and automatically restart the cupsd daemon. This step is extremely important; you have to update the printer settings and restart the cupsd daemon to force it to reread your new settings. Click Quit from the File menu when finished.

## Related Ubuntu and Linux Commands

The following commands help you manage printing services:

- accept—Controls print job access to the CUPS server via the command line
- cancel—Cancels a print job from the command line
- cancel—Command-line control of print queues
- disable—Controls printing from the command line
- enable—Command-line control CUPS printers
- lp—Command-line control of printers and print service
- lpq—Displays status of printers and print service at the console
- lpq—Views print queues (pending print jobs) at the console
- lprm—Removes print jobs from the print queue via the command line
- lpstat—Displays printer and server status
- system-config-printer—Ubuntu's graphical printer configuration tool

# CHAPTER 9

# Games

## IN THIS CHAPTER

- Linux Gaming
- Installing Games for Ubuntu
- Playing Windows Games with Cedega
- Reference

Whether your boss likes it or not, gaming is a huge part of computing. For any operating system to have true mass market appeal, it must have the ability to play games. From the humble card games that entertain millions during their coffee breaks, to the heavily involved first-person shooters that involve players dotted around the globe, Linux offers a gaming platform that may surprise even the hardened Windows fanboy.

In this chapter we’ll explore some of the common games available for you to download and install. We’ll even show you how to get your Windows-based games running under Linux.

## Linux Gaming

A number of games come as part of Ubuntu, and they are divided into three distinct camps: KDE games, GNOME games, and X games. Our favorites are Planet Penguin Racer and Torc (see Figure 9.1), but there are a few others for you to choose from. The best part, of course, is trying each one and seeing what you think. Many other free games are available across the Web, so go to Google and see what you come up with.

However, games for Linux do not stop there—a few versions of popular Windows-based games have been across to the Linux platform, including DOOM 3, Unreal Tournament 2004, and Quake 4. These three popular games have native Linux support and in some cases can run at similar, if not better, speeds than their Windows counterparts. There’s
