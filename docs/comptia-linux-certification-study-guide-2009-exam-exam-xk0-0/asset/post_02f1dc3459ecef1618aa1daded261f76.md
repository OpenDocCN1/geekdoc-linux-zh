
which is updated using `apt-get update`, to update all installed applications to their most current versions.

Incorrect answers and explanations: **A, C**, and **D**. Answer **A** is incorrect because it is the command to update the APT database. Answer **C** is incorrect because the `dist-upgrade` option upgrades the entire distribution to the latest version and the requirements in this question ask for only the installed applications to be updated. Answer **D** is incorrect because, when a package name is specified, it is the command to install an individual application.

## CHAPTER 8: INSTALLING, CONFIGURING AS A WORKSTATION

- 1. A user has sent three jobs to a printer, with job numbers **372**, **373**, and **374**. They now want to remove printer job number **373**, which has not been printed yet. Which command will achieve this?
    - A. `lpr --cancel 373`
    - B. `lpstat -c 373`
    - C. `cancel 373`
    - D. `lpr -c 373`

Correct answer and explanation: **C**. The correct answer is **C** as the `cancel` command will cancel the given job provided it is still in the queue and the user is the owner or has the correct permissions.

Incorrect answers and explanations: **A, B**, and **D**. Answers **A** and **D** are incorrect as the `lpr` command submits jobs to a printer. Answer **B** is incorrect as the `lpstat` command will display the status of a printer.

- 2. A user is running KDE as his display environment. What will be the most likely environment variable for the display manager?
    - A. `DISPLAYMANAGER="KDE"`
    - B. `DISPLAYMANAGER="kdm4"`
    - C. `DISPLAYMANAGER="kde_display"`
    - D. `DISPLAYMANAGER="gdm"`

Correct answer and explanation: **B**. The correct answer is **B** as this will specify version 4 of the K Display Manager.

Incorrect answers and explanations: **A, C**, and **D**. Answer **A** is incorrect as KDE is the overall K Desktop Environment and not the display manager. Answer **C** is wrong as this does not define K Display Manager. Answer **D** is incorrect as this refers to the GNOME display manager.

- 3. A user is sending a job to printer `EPSON_COLOR`, which is not their default printer. They want it printed with a banner title of *myjob* and then a mail is sent to let them know when it has been printed. The user will need to use the following command:
    - A. `lpr -m -T myjob -P EPSON_COLOR`
    - B. `lpr -sendmail -C myjob -P EPSON_COLOR`
    - C. `lpr -m -T myjob`
    - D. `lpr -sendmail -T myjob -P EPSON_COLOR`

Correct answer and explanation: **A.** Answer **A** is correct as this sends a mail to the user with the `-m` option, prints the title *myjob* on the banner page, and sends it to printer `EPSON_COLOR`.

Incorrect answers and explanations: **B, C, and D.** Answer **C** is incorrect as this will send the print job to the default printer, which is not `EPSON_COLOR`. Answer **B** is incorrect as there is no `-sendmail` option and the `-C` option prints the class as the job classification on the banner page. Option **D** is incorrect as there is no `-sendmail` option.

- 4. A normal user wants to disable a printer in the CUPS Web interface. What do they need to do to achieve this?
    - A. Enter the superuser user name and password when prompted by CUPS
    - B. Open a terminal window and enter the superuser name and password before launching the Web browser
    - C. Start CUPS with the `-s` option
    - D. Start CUPS and enter the superuser name and password in the **Authentication** tab

Correct answers and explanations: **A.** Answer **A** is correct. CUPS will prompt the user for a username and password before a printer can be disabled. This is typically the *superuser password* or an administrative account with the appropriate privileges.

Incorrect answers and explanations: **B, C, and D.** Answer **B** is incorrect as this will not pass the superuser credentials to the CUPS application. Answer **C** is incorrect as there is no `-s` option. Answer **D** is incorrect as there is not an authentication tab in the CUPS interface.

- 5. The main X Windows configuration file *xinitrc* is likely to be located in which system directory when GNOME has been installed as the only display manager?
    - A. /etc/X11
    - B. /X1
    - C. /usr/X11
    - D. User's home directory

Correct answer and explanation: D. Answer D is correct as X Windows will always look in the user's home directory first and will use this configuration file if it is there.

Incorrect answers and explanations: A, B, and C. Answers B and C are incorrect as there are not any directories with that name defined as a standard. In addition, A is incorrect as the configuration file is not normally located there.

- 6. Which of the following would be the best description of the X Windows System if you were describing it to a new Linux user?
    - A. X Windows is a client-server architecture, with the client accepting keyboard input.
    - B. X Windows is a client-server architecture, with the server accepting keyboard input.
    - C. X Windows is a client-server architecture and cannot be ported to run on a Microsoft Windows system.
    - D. Both the X Windows server and client must be on the same system.

Correct answer and explanation: B. Answer B is correct as the X server accepts the input from the keyboard and mouse. In an X-server environment, the server provides display and I/O services to the applications.

Incorrect answers and explanations: A, C, and D. Answer A is incorrect as the clients in an X-server environment are the applications. Answer C is incorrect as X windows is platform independent. There are versions that can run on a multitude of operating system and can run on Microsoft Windows XP and Vista. Answer D is incorrect as the client and server may be on different systems.

- 7. A system administrator wants to add remote displays to systems configured with X Windows. Which protocol and port will be used between the X server and the remote client?
    - A. XDMF normally running on port 177
    - B. XDMCP normally running on port 177
    - C. XDMF normally running on port 187
    - D. XDMCP normally running on port 187

Correct answer and explanation: B. The correct answer is B as the protocol is XDMCP and the correct port 177.
Incorrect answers and explanations: A, C, and D. Answer A is incorrect as XDMF is not a valid protocol. Answer C is incorrect as XDMF is not a valid protocol and the port is incorrect. Answer D is incorrect as protocol XDMCP is correct but the port is incorrect.

- 8. A user has installed Linux on his/her system and has made KDE his/her default desktop manager. What is the default number of virtual desktops and the maximum number that can be configured by the user?
    - A. Default of four desktops and a maximum of 36
    - B. Default of two desktops and a maximum of 36
    - C. Default of two desktops and no maximum
    - D. Default of two desktops and the user cannot configure any more

Correct answer and explanation: A. Answer A is correct as KDE will normally default to four virtual desktops and the maximum allowable is 36.
Incorrect answers and explanations: B, C, and D. Answer B is partially correct in that the maximum is 36 desktops, but the default is four virtual desktops. Answer C is incorrect as the default is two and the maximum allowable is 36. Answer D is incorrect as there is a default of four virtual desktops and this can be increased to 36 by the user.

- 9. A company has installed Linux with the GNOME desktop on a number of older systems as a means to extend their life. These systems use an 800 × 600 display and have a maximum of 64 MB of RAM installed. They want to use these systems as remote terminal emulators to a more powerful X server on another system. Which remote terminal would give the best performance due to its small memory footprint?
    - A. kconsole
    - B. gconsole
    - C. gnome-terminal
    - D. xterm

Correct answer and explanation: **D**. Answer **D** is correct as `xterm` has a very small memory footprint (less than 1 MB) and is therefore likely to give the best overall performance.

Incorrect answers and explanations: **A**, **B**, and **C**. Answer **A** is incorrect as this is the normal `console` in KDE and GNOME is installed. Answer **C** is incorrect as the `gnome-terminal` has a much larger memory footprint than `xterm`. Answer **B** is incorrect as there is not a `gconsole` program as standard within GNOME.

- 10. A user is configuring his/her Linux system, which has KDE installed on it. The user wishes to add a new printer and will do so through the CUPS Web interface. The user has installed Firefox and the CUPS server on his/her system and both are working correctly. What would be the best way to access the CUPS server?
    - A. CUPS can only be accessed from the command line using the command `CUPS -S` when it is installed locally.
    - B. CUPS can be accessed using Firefox with the URL `http://localhost:631`.
    - C. CUPS can be accessed using Firefox with the URL `http://631:localhost`.
    - D. CUPS can be accessed using Firefox with the URL `http://cups@localhost`.

Correct answer and explanation: **B**. Answer **B** is correct as the CUPS server is hosted locally and the normal port it runs on is 631.

Incorrect answers and explanations: **A**, **C**, and **D**. Answer **A** is incorrect as CUPS is accessed normally from the Web interface. Answer **C** is incorrect as the URL is formatted incorrectly, the correct notation being `address:port`. Answer **D** is incorrect as no port is specified, and the URL looks more like a e-mail address.

- 11. A user has problems with the startup of his/her system and he/she wishes to start up his/her system up in single user mode and then to start X Windows. Which is the best method to achieve this?
    - A. Start the system in run level 1 and then run `startx`
    - B. Start the system in run level 5 and then run `startx`
    - C. Reboot the system and when the initial load screen appears, type `Ctrl` and `S` together
    - D. Reboot the system and when the initial load screen appears, type `Ctrl` and `1` together
