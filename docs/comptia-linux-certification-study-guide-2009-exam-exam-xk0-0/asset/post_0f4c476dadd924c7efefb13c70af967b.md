
interface for a user. However, for systems that have a smaller amount of random access memory (RAM), there is another emulator called xterm, which has a very small memory footprint (usually under 1 MB), although the window is smaller and the default font is hard to read. The standard xterm emulations are for DEC VTxxx and Tektronix 4014 terminals.

The VTxxx and Tektronix terminals can each have their own window so that a user can edit text in one and look at graphics in another. Only one of these windows will be considered active at any one time, and this one will accept keyboard input and terminal output. The number of options allowed for xterm is very large, which will allow the system to correctly emulate the terminal and application running in it.

## SUMMARY OF EXAM OBJECTIVES

In this chapter, you have learned about how to configure a Linux system when it is used as a workstation. The two most common aspects of the user experience – namely, printing and the GUI (X Windows interface) – were explained, and how these can be configured for individual users.

In spite of the move toward the paperless office, printing letters and other documents is still a firm requirement for most users. With the move to digital photography, the home user is now often using their printer more than in previous years. The setup and use of a printer in Linux is slightly more difficult than in the “plug and play” world of Microsoft Windows, but the use of the CUPS interface is now making this a much easier task.

The CUPS interface was shown, and how to add local printers using the interface. The management of printers and their queues was demonstrated using the CUPS interface, and also how this could be achieved using the command line interface.

The users’ main interface to the computer is through the GUI, and the number of different interfaces that can be used is very large. The standard, underlying interface is X Windows, currently at version 11, which is commonly known as X11. This can be used and enhanced with many different display managers, the two most common ones being GNOME and KDE.

The main configuration files for X Windows were described, and how to modify these for individual users. Specific configuration details were then outlined for the GNOME and KDE desktops. The use of multiple or virtual desktops were explained, and how these may be different from a user’s experience of a single desktop. The configuration of these multiple desktops was explained.

## SELF TEST

1. A user has sent three jobs to a printer, with job numbers 372, 373, and 374. They now want to remove printer job number 373, which has not been printed yet. Which command will achieve this?
   - **A.** `lpr --cancel 373`
   - **B.** `lpsat -c 373`
   - **C.** `cancel 373`
   - **D.** `lpr -c 373`

2. A user is running KDE as his display environment. What will be the most likely environment variable for the display manager?
   - **A.** `DISPLAYMANAGER="KDE"`
   - **B.** `DISPLAYMANAGER="kdm4"`
   - **C.** `DISPLAYMANAGER="kde_display"`
   - **D.** `DISPLAYMANAGER="gdm"`

3. A user is sending a job to printer EPSON_COLOR, which is not his or her default printer. They want it printed with a banner title of *myjob* and then a mail to be sent to let them know when it has been printed. The user will need to use the following command:
   - **A.** `lpr -m -T myjob -P EPSON_COLOR`
   - **B.** `lpr -sendmail -C myjob -P EPSON_COLOR`
   - **C.** `lpr -m -T myjob`
   - **D.** `lpr -sendmail -T myjob -P EPSON_COLOR`

4. A normal user wants to disable a printer in the CUPS Web interface. What do they need to do to achieve this?
   - **A.** Enter the superuser username and password when prompted by CUPS.
   - **B.** Open a terminal window and enter the superuser name and password before launching the Web browser.
   - **C.** Start CUPS with the `-s` option.
   - **D.** Start CUPS, and enter the superuser name and password in the *Authentication* tab.

5. The main X Windows configuration file *xinitrc* is likely to be located in which system directory, when GNOME has been installed as the only display manager?
   - **A.** `./etc/X11`
   - **B.** `X11`
   - **C.** `./usr/X11`
   - **D.** *User’s home directory*

6. Which of the following would be the best description of the X Windows System if you were describing it to a new Linux user?
   - **A.** X Windows is a client-server architecture, with the client accepting keyboard input.
   - **B.** X Windows is a client-server architecture, with the server accepting keyboard input.
   - **C.** X Windows is a client-server architecture and cannot be ported to run on a Microsoft Windows system.
   - **D.** Both the X Windows server and client must be on the same system.

7. A system administrator wants to add remote displays to systems configured with X Windows. Which protocol and port will be used between the X server and the remote client?
   - **A.** *XDM*P normally running on port 177
   - **B.** *XDMCP* normally running on port 177
   - **C.** *XDM*P normally running on port 187
   - **D.** *XDMCP* normally running on port 187

8. A user has installed Linux on his or her system and has made KDE as the default desktop manager. What is the default number of virtual desktops, and the maximum number that can be configured by the user?
   - **A.** Default of four desktops and a maximum of 36
   - **B.** Default of two desktops and a maximum of 36
   - **C.** Default of two desktops and no maximum
   - **D.** Default of two desktops and the user cannot configure any number

9. A company has installed Linux with the GNOME desktop on a number of older systems as a means to extend their life. These systems use an 800×600 display and have a maximum of 64 MB of RAM installed. They want to use these systems as remote terminal emulators to a more powerful X server on another system. Which remote terminal would give the best performance due to its small memory footprint?
   - **A.** konsale
   - **B.** gconsole
   - **C.** gnome-terminal
   - **D.** xterm

10. A user is configuring his or her Linux system, which has KDE installed on it. The user wishes to add a new printer and will do so through the CUPS Web interface. The user has installed Firefox, and the CUPS server on the system and both are working correctly. What would be the best way to access the CUPS server?
    - **A.** CUPS can only be accessed from the command line using the command `CUPS -S` when it is installed locally
    - **B.** CUPS can be accessed using Firefox with the URL `http://localhost:631`
    - **C.** CUPS can be accessed using Firefox with the URL `http://631:localhost`
    - **D.** CUPS can be accessed using Firefox with the URL `http://cups@localhost`

11. A user has problems with the startup of his or her system, and the user wishes to start up the system in single-user mode and then to start X Windows. Which is the best method to achieve this?
    - **A.** Start the system in run level 1, and then run `startx`.
    - **B.** Start the system in run level 5, and then run `startx`.
    - **C.** Reboot the system, and when the initial load screen appears, type `Ctrl` and S together.
    - **D.** Reboot the system, and when the initial load screen appears, type `Ctrl` and 1 together.

12. You have just downloaded and installed the latest version of the GNOME desktop. This is a beta version, and your system seems to freeze when you start it. Which option would be worst one to use?
    - **A.** Press the `reset` button, and boot into single-user mode with command-line input. Then, remove the beta version.
    - **B.** Open a terminal window and type `shutdown -now`, and then boot into single-user mode with command-line input. Then, remove the beta version.
    - **C.** Type `Ctrl` + `Alt` + `F2`, and use the root username and password when prompted. Look at the PID list and kill all the processes associated with X Terminal session. You can now uninstall the beta version.
    - **D.** Type `Ctrl` + `Alt` + `F7`, and use the root username and password when prompted. Type `rollback X11` to revert to the previous version of X Windows.
