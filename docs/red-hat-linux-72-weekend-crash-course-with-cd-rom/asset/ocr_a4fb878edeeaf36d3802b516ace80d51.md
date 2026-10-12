+   15. Ghostscript is a nearly complete implementation of the PostScript language that enables you to print PostScript documents on many non-PostScript devices.
+   16. The name of the spreadsheet application is Gnumeric. Gnumeric’s default file format is XML (eXtensible Markup Language). Gnumeric can exchange files with Microsoft Excel.
+   17. You would use the command `aspell check report.txt` to check the spelling of a text file named `report.txt`.
+   18. The Red Hat Network is a system management tool consisting of Software Manager. Software Manager provides several services, including a software update subscription service, automatic RPM updates, and e-mail notification of bugs and security alerts.
+   19. First, you must create a system profile, and then register it with the Red Hat Network by sending the file to Red Hat. Next, you have to log in to the Red Hat Network and activate your Software Manager subscription.
+   20. Log in as root, and select Main Menu Program System Update Agent from the GNOME desktop. Then select the updates, if any are available, that you wish to install on your system. Start the download and installation process by following Update Agent’s prompts.

# Sunday Morning Review Answers

+   1. The X server is a process that manages a bitmapped display, a keyboard, and a mouse. The X server controls the monitor, the keyboard, and the mouse on behalf of X clients requesting some sort of input or output activity using those devices, such as a request to open a window.
+   2. The X configuration file is /etc/X11/XF86Config-4. You can use xf86config, X86cfg, or Kconfigurator to create a new X configuration file.
+   3. The X graphical screen is partially working, press Ctrl+Alt+F1 to switch to the text console and log in as root at the text login prompt. Then type telinit 3 to kill the running X server. Next, create a new X configuration file, and type telinit 5 to restart the graphical display manager. Finally, type Ctrl+Alt+Backspace to kill the X server and run it to restart with the new configuration file.
+   4. The init runs all other processes on the system. It starts at boot time and is primarily responsible for starting system daemons that provide essential services, and mounting file systems. The contents of /etc/inittab file control init’s behavior.
+   5. Look for the line with the keyword initdefault in the third field of /etc/inittab file; the fields are separated by colons (:). The second field of this line specifies the default run level.
+   6. The init process runs the /etc/rc.d/rc.sysinit script. This script, in turn, runs many other scripts from the subdirectories in /etc/rc.d, especially /etc/rc.d/init.d.