Correct answer and explanation: **A**. Answer **A** is correct as this will start Linux in single user mode on most Linux distributions and will then allow the user to start X Windows when the command prompt appears.

Incorrect answers and explanations: **B**, **C**, and **D**. Answer **B** is incorrect as run level 5 normally starts X Windows at the end of the boot process. Answers **C** and **D** are incorrect as these commands are not available.

12.  You have just downloaded and installed the latest version of the GNOME desktop. This is a beta version and our system seems to freeze when you start it. Which option would be the worst one to use?

+   A.  Press the reset button and boot into single user mode with command-line input. Then remove the beta version.
+   B.  Open a terminal window and type `shutdown -now` and then boot into single user mode with command-line input. Then, remove the beta version.
+   C.  Type `Ctrl + Alt + F2` and use the root username and password when prompted. Look at the PID list and kill all the processes associated with X Terminal session. You can now uninstall the beta version.
+   D.  Type `Ctrl + Alt + F7` and use the root username and password when prompted. Type `rollback` X11 to revert to the previous version of X Windows.

Correct answer and explanation: **C**. Answer **C** is the correct answer. This will revert you to a terminal window where you can gracefully kill the rogue X Windows sessions and then remove the beta software.

Incorrect answers and explanations: **A**, **B**, and **D**. Answer **A** is incorrect as this will result in the loss of files that have not been written to the disk and possible disk corruption. It should only be used as a last resort. Answer **B** is also incorrect as this will also shut the system down immediately with the same consequences as **A**. Answer **D** is incorrect as there is not a `rollback` command to revert software back to a previous version.

13.  You want to run the GNOME window manager if you boot your system into runlevel 5 and the Openbox window manager if you start the system in run level 4. How can this be best achieved?