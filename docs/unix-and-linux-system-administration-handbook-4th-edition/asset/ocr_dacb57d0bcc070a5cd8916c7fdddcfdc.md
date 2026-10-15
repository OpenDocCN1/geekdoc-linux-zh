# Exhibit A The X client/server model

![](bbox=[0.18, 0.19, 0.85, 0.42])

Application developers have their choice of several common widget libraries and user interface standards. Unfortunately, the choice often depends more on religious affiliation than on any real design considerations. Although freedom of choice is good, X's UI agnosticism and lack of design leadership did result in many years of poor user interfaces. Fortunately, the fit and finish of the mainstream X environments has improved markedly. Both the KDE and GNOME desktop environments sport modern web browsers, user-friendly file managers, and modern multimedia capabilities.

In this chapter, we explain how to run programs on a remote display and how to enable authentication. We then discuss how to configure the X.Org server and how to troubleshoot configuration errors. Finally, we touch briefly on some of the available window managers and desktop environments.

# 25.1 THE DISPLAY MANAGER

The display manager presents the user with a (graphical) login screen and is usually the first thing a user sees when sitting down at the computer. It is not required; many users disable the display manager and start X from the text console or from their .login script by running startx (which itself is a wrapper for the xinit program, which starts the X server).

xdm (for X display manager) is the original display manager, but modern replacements such as gdm (the GNOME display manager) and kdm (the KDE display manager) deliver additional features and are more aesthetically pleasing. The display manager can manage remote logins to other X servers through the XDMCP protocol, and it can also handle display authentication (see Client authentication on page 1016).

Configuration files in the xdm, gdm, or kdm subdirectory of /etc/X11 specify how the display manager will run. For example, you can edit the Xservers file to change the display number used for this server if multiple servers will be running