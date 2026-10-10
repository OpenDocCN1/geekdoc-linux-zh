the monitor's controls. If this fails to give satisfactory results you can use the Xrdump program to make fine adjustments to the scan rates and other aspects of the video timing. I suppose that using Xrdump is very slightly risky, so it is best to only use it if you really need to.

# **Testing, testing**

Eventually you should end up with everything installed and Linux under way. Before you can use Linux it is necessary to log in, and this requires a user name and the corresponding password. If you set up a user account during the installation process enter the appropriate name and press Return. Then when prompted for the password, enter the appropriate string of characters and press Return. You should then be in to Linux and ready to start using the new operating system. If you did not set up a user account during installation it is still possible to go into Linux. You must log in as the system supervisor. For the user name enter “root” and then press Return. Then type in the password and press Return again. Linux will then be up and running, awaiting your first commands.

At this point it is a good idea to close down Linux, switch off the computer, “cold start” it again to do so, go through the installation process again, making sure that the appropriate disc partition is bootable, etc. It is not a good idea to shut down Linux by simply switching off the computer. As with Windows 95 and 98, this leaves various temporary files on the hard disc drive, and things left somewhat “up in the air”. The correct way to close down Linux is to use the shutdown command, and to only switch off the computer once the string of on-screen messages finish. The first message should say something like “system halted”.

The shutdown command has various switches and controls that can be used to govern the exact way in which it functions. Bear in mind here that Linux is designed for use with a network that will probably be switched off would normally be issued together with a shutdown time and a message. All this is of no consequence if Linux is used on a workstation, warning of the shutdown time would then be sent to each terminal. When you simply want to close down the system immediately at the end of each session. For an immediate shutdown use this command:

```
shutdown -h now
```



Linux is usually case sensitive, and the command examples given in this book will only work if they are copied precisely, but there are some exceptions. The text will be in lower case letters, but if in some cases everything had been written in lowercase then the system successfully the next step is to check that X windows is functioning correctly. By default Linux does not usually run X windows automatically at start-up. But some systems do now it so. to start X Windows use this command:

```
startx
```

After a few seconds of frantic hard disc activity a graphical user interface should appear on the screen, and the screen's exact appearance will depend on the distribution and version of Linux in use. Figure 1.12 and 1.13 respectively show the screens obtained from Red Hat Linux 5.2 and Caldera Open Linux 1.3. It is worthwhile experimenting with the general way in which systems and the mouse. However, if an alternative desktop environment such as KDE is included in the installation, I would suggest extending X Windows before trying such a thing in the normal start-up. If KDE or an alternative such as Gnome is available during installation. I would strongly recommend including it in the installation. Most Linux

![](bbox=[0.55, 0.45, 0.85, 0.7])

Fig. 1.12 The opening X Windows screen in Red Hat Linux 5.2