+   • **KDE Control Center**: Click on the button with an icon of a terminal covered by a circuit board to start the KDE Control Center. The Control Center enables you to configure various aspects of the KDE desktop.
+   • **Online Help**: To read the online help on KDE, click the button with an icon of a book.
+   • **File Manager**: To view the contents of your home directory, click the button with the icon of a folder and a home.
+   • **Virtual Desktop**: KDE supports a virtual desktop. By default, you get four virtual desktops. You can click one of the buttons labeled 1, 2, 3, 4 or 5 to switch to a specific desktop. You can use the desktops to organize your application windows. You do not need to clutter up a single desktop with many open windows. When a desktop gets crowded, simply switch to another desktop and open the applications there.

To log out of KDE, select K-C Logout and click the Logout button on the resulting dialog box. The next section shows you how to shut down Red Hat Linux and power off your PC.

![](bbox=[0.04, 0.42, 0.12, 0.51])

**10 Min. To Go**

# ## Shutting Down Red Hat Linux

When you are ready to shut down Red Hat Linux, you must do so in an orderly manner. Even if you are the sole user of a Linux system, several other programs are usually running in the background. Also, operating systems such as Linux try to optimize the way that they write data to the disk. Because disk access is relatively slow (compared to the time needed to access memory locations), data generally is held in memory and written to the disk in large chunks. Therefore, if you simply turn off the power, you run the risk of some files not updating properly.

Any user (you do not have to be logged in) can shut down the system from the desktop or the graphical login screen. The **System** menu in the Login dialog box provides menu options for rebooting or halting the system. To shut down the system, simply select System-C Halt in the graphical login screen of Figure 3-1.

Another dialog box asks you to confirm if you really want to halt the system. Click the **Yes** button. The system then shuts down in an orderly manner.

As the system shuts down, you see messages about processes being shut down. You may be surprised at how many processes there are, even though no one is explicitly running any programs on the system. If your system does not automatically power off on shut down, you can manually turn off the power.

# ## Troubleshooting

One of the most common problems when installing Red Hat Linux is not being able to log in after the post-installation reboot. If you did not create a user account during the installation, you must log in as root and create a user account as described in Session 10. Similarly, if you forgot the user account password you created during installation, log in as the root user, then use the techniques described in Session 10 to change the password for that user account.

If you forgot the root password, reboot and follow these steps: