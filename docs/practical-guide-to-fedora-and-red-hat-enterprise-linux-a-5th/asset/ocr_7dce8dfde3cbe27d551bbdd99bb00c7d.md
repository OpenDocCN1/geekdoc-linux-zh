![](bbox=[0.29, 0.1, 0.81, 0.46])

**Figure 3-3**  **A GNOME Live desktop**

in as the user named **liveuser**, and displays the GNOME desktop (Figure 3-3). To speed up this process, you can click the button labeled **Log In** when Fedora displays the login screen.

KDE If you are installing from Fedora KDE Live Media, you are installing the KDE desktop manager. When you boot from this disk, Fedora next displays a KDE startup screen and then the KDE desktop—there is no need to log in.

**optional** **SEEING WHAT IS GOING ON**

If you are curious and want to see what Fedora is doing as it boots from a Live CD, remove **quiet**, which controls kernel messages, and **rhgb** (Red Hat graphical boot), which controls messages from the graphical installer, from the boot parameters. See Figure 3-13 on page 68; the list of parameters on the screen will be different from those in the figure. With the Fedora Live Welcome menu displayed (Figure 3-2), press **TAB** to display the boot command-line parameters. Use the **BACK ARROW** key to back up over—but not remove—any words to the right of **quiet**. Press **BACKSPACE** or **DEL** to back up over and erase **quiet** and **rhgb** from the boot command line. Press **RETURN**. Now as Fedora boots, it displays information about what it is doing. Text scrolls on the screen, although sometimes too rapidly to read. When you boot Fedora from a DVD and when you boot RHEL, this information is displayed by default: You do not have to change the command line.