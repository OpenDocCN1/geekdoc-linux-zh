Changing the Window Manager or Desktop Environment

Chapter 6 describes various system startup scripts, including two that are likely to be used to launch a window manager: .xinitrc and .xsession. These scripts reside in a user’s home directory and are run when a user starts X from a text mode login or logs in using the XDM GUI login tool, respectively. To launch a particular window manager or desktop environment, it’s necessary to include a reference to the relevant program in the startup script. Chapter 6, and in particular the “GUI Login Control Files” section, provides more details concerning this configuration.

Some replacements for the XDM login program, such as the GNOME Desktop Manager (GDM) and the KDE Display Manager (KDM) provide users with a choice of desktop environments at login. For instance, Figure 13-6 shows the GDM GUI login tool. The Session menu item in this tool provides a number of options, including Xsession (which runs the user’s .xsession script), Gnome (which launches GNOME), and Failsafe xterm (which launches a minimal desktop environment). Both GDM and KDM remember the user’s last selection on subsequent logins, so they’re a good way to enable less experienced users to customize their login options, at least within the parameters of these tools’ configurations. Chapter 21 describes the configuration of GUI login programs in more detail.

![](bbox=[0.13, 0.53, 0.85, 0.85])

> **Figure 13-6.** Some GUI login tools provide a means to select the window manager or desktop environment when a user logs in.