# Setting the Terminal Type

In most instances, the vi editor will function properly when you first attempt to use it. This is particularly true when you use a Solaris workstation like Sun Ultra, where the display is full featured and properly specified in system configuration. In certain situations, you may find that vi doesn’t display or update on a terminal correctly. Different terminals use different control codes and vi needs to know which terminal it is working with in order to know what codes are appropriate. Typically, an administrator will set up this parameter for you, but it is relatively straightforward to set the parameter yourself.

You can enter the terminal type from within vi and that terminal type will be used for the terminal session, or you can specify the terminal type parameter using the $TERM variable as part of a shell’s login script. Many terminals will prompt you to confirm the terminal type during login, as in TERM = (vt100), or allow you to change the terminal type at login.

To see what your system thinks is the current terminal, follow these steps:

+   1.  Type `echo $TERM` at the system prompt.
+   2.  Press the Return key.

If you don’t get the answer you expect or if you are using the Bourne or Korn shell, you can use the TERM=<name> command followed by the export name command to replace the terminal type. When you use one terminal type consistently, put these commands in your .profile file. For the C shell, you will need to use the setenv TERM <name> command. The <name> variable is replaced with the name of your terminal, and the command line for the console in the CDE using the C shell would be % sentenv TERM dtterm. You can also put this command into your .login file.

Solaris supports both terminfo and tercap name styles that are part of System V or BSD. The following terminals are in common use:

+   - dtterm (CDE from the console)
+   - sun-cmd (OpenLook from the console)
+   - VT100, using a terminal emulator
+   - xterm or VS100 (when you are on an X-terminal)

If you are unsure of what terminal to use, try the VT100 because most displays will support this emulation. For PCs and Macs, you may find that you can run applications using either the VT100 or VT220 terminal emulation.

# Spawning a Shell

You can spawn a shell from within a vi editing session if you need to check your e-mail, do housekeeping on files, set system parameters, or execute a particular command from