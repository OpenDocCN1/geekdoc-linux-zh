to the Login screen (or the command line if you started your GUI from there). Also, from the GDM, you can shift to the command line interface with the CTRL-ALT-F1 keys, and then shift back to the GUI with the CTRL-ALT-F7 keys.

When the GDM starts up, it shows a login window with a box for login. Four pop-up menus are located at the bottom of the screen, labeled Session, Language, Shutdown, and Restart. To log in, enter your username in the box labeled Username and press ENTER. You are prompted to enter your password. Do so, and press ENTER. By default, the GNOME desktop is then started up.

When you log out from the desktop, you return to the GDM login window. To shut down your Linux system, click the System menu to display the entry Reboot or Shutdown. Select Shutdown to shut down your system. Alternatively, you can also shut down when you log out from GNOME. GNOME will display a logout screen with the options Logout, Shutdown, or Reboot. Logout is the default, but selecting Shutdown will also shut down your system. Selecting Reboot will restart your system. (You can also open a terminal window and enter the shutdown, halt, or reboot command as described in the next section; halt will log out and shut down your system.)

From the Session menu, you can select the desktop or window manager you want to start up. Here you can select KDE to start up the K Desktop, for example, instead of GNOME. On Red Hat, both KDE and GNOME will use an interface with a Bluecurve look and feel, appearing much the same. The Language menu lists a variety of different languages that Linux supports. Choose one to change the language interface.

# Accessing Linux from the Command Line Interface

For the command line interface, you are initially given a login prompt. The system is now running and waiting for a user to log in and use it. You can enter your username and password to use the system. The login prompt is preceded by the hostname you gave your system. In this example, the hostname is turtle. When you finish using Linux, you first log out. Linux then displays exactly the same login prompt, waiting for you or another user to log in again. This is the equivalent of the login window provided by the GDM. You can then log into another account.

```
Fedora Core release 1
Kernel 2.4.22-1 on an i686

turtle login:
```

# Logging In and Out

Once you log in to an account, you can enter and execute commands. Logging in to your Linux account involves two steps: entering your username and then entering your password. Type in the username for your user account. If you make a mistake, you can erase characters with the BACKSPACE key. In the next example, the user enters the username dylanp and is then prompted to enter the password:

```
Fedora Core release 1
Kernel 2.4.22-1 on an i686

turtle login: dylanp
Password:
```