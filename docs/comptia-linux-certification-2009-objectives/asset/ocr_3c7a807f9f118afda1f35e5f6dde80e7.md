+   3.  Change the location of the xterm window in the screen.
    a.  Enter vi /etc/X11/xinit/xinitrc.
    b.  Scroll down and change xterm -geometry 80x50-50+150, which sets the location of the xterm window in the screen, to xterm -(Parameter) {Value}.
    c.  Save and close the file.

![](bbox=[0.095, 0.195, 0.755, 0.275])

+   4.  Log out from the current session.
5.  Reboot the system to verify that the system boots on the specified desktop.
6.  Click Session, choose Failsafe Terminal and click OK.
7.  Enter the user name and password to display the xterm X terminal. Ensure that the cursor is within the xterm window.
8.  Enter exit to log out and return to the login screen.

![](bbox=[0.065, 0.435, 0.755, 0.51])

# Procedure Reference: Verify and Resolve Library Dependency Issues for X Applications

To verify and resolve dependency issues for X applications:

+   1.  Enter rpm -qR {X application package name} to identify the library files and the dependent packages needed for the installation of the X package.
2.  Enter locate {library file} to verify that the library files are present in the system.
3.  Enter rpm -ivh {X application package name} to install all the dependencies and then install the required X application packages.

# Importance of Library Files

During the installation of certain X applications, the application will search for library files and some dependent packages needed for the X application package to be successfully installed on a system. In case the library files are not installed on the system, you need to first identify the library files and then install the packages containing them along with the dependent packages required for the X application.