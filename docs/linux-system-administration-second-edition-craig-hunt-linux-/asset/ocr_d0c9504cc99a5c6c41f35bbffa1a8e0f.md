![](bbox=[0.1, 0.04, 0.85, 0.3])

Figure 13.5: Some window managers have their own unique looks and provide unusual feature sets.

# Setting the Window Manager

Window manager preference is a very personal matter. If you want to experiment, you can try several different window managers to see which you prefer. Linux distributions use a configuration script in the user’s home directory to run programs the user wants to run at login time. If this file is absent, the system uses a default script. The name of this script varies with your login preferences, but it’s usually located in the /etc/X11 directory tree, often in /etc/X11/xinit. On Red Hat 7.3, the user-customizable configuration script is called .xsession, and it must have execute permissions. Other distributions may call this script other things, such as .Xlogin. When launching X from a text-mode login via startx, yet another script is commonly used: .xinitrc. To replace the default set of login actions with something else, follow these steps:

+   1. Load the .xsession or other X configuration file from your home directory into a text editor (on a fresh account, this file won’t exist, so you may need to tell your editor to create it).
2. Type the names of any programs you want to run automatically when you log in, including your window manager. If you want a program to run and stay running while other programs run, be sure to follow its startup line with an ampersand (&), or the script will stop running until you’ve closed that program. In most cases, the final program launched from .xinitrc should be your window manager, and it should not include an ampersand. This way, when you exit from the window manager, you’ll log off the account. As an example, the following file launches an xterm window and the wm2 window manager:

    ```
    xterm &
    wm2
    ```
3. Save the .xsession file and exit from the text editor.
4. Type `chmod 755 ~/.xsession` to give the file execute permissions. (You can use more restrictive permissions, such as 0700, if you don’t want others to see which programs you run automatically.)

Thereafter, when you log on, Linux will launch whichever programs (including the window manager) you set in the .xsession file when you log on again in X. You may, however, have to select a particular login option in your XDM program. If you use KDM, for example, you often choose Default from the drop-down list of Session Types. If you don’t know where to begin in your exploration of window managers, an excellent starting point is the window managers Web site at http://www.plig.org/xwinman/ . This site features descriptions of the most common window managers