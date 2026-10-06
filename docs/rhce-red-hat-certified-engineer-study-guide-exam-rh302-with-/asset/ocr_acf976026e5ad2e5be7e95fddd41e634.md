The script checks for a ~/.wm_style file containing the name of the manager to be run and launches the specified window manager. If that file is not present, the script launches the FVWM95 window manager. If the script cannot launch the FVWM95 window manager—perhaps it is not installed—the script launches FVWM or TWM, a very small and efficient window manager installed as part of the XFree86 package.

Now perform Exercise 27.2, which asks you to choose a window manager.

# EXERCISE 27.2
Choosing a Window Manager

As explained, the ~/.wm_style file specifies the name of your window manager. Perform these steps to experiment with changing the window manager.

+   1. If FVWM95 is not installed, install it.
2. Use ~/.wm_style to specify FVWM95 as your window manager. Exit and reboot X to verify that your selection operates properly.

You can consult this book or other documentation to help you in completing this exercise. But, before taking the RHCE exam, be sure you can choose a window manager without consulting books or notes.

# Display Managers

Red Linux lets you choose among three display managers:

+   - GDM, a display manager associated with GNOME
- KDM, a display manager associated with KDE
- XDM, a display manager distributed as part of XFree86

All three display managers can be used with a variety of desktop environments. For example, you can use the GDM display manager with AnotherLevel, GNOME, or KDE. Both GDM and KDM are highly configurable. The XDM display manager is not highly configurable, but it is more robust than GDM or KDM when used to support remote X logins, which is explained in Chapter 28, “Configuring and Using Remote X Servers and Clients.”