blank area of your desktop (that is, an area without a window) and left-click. You are presented with a root menu. You then scroll down to a selection similar to *Exit <window manager>* and hold the mouse in that position or even left-click. A second part of the menu might appear (depending on the window manager). It might ask you whether your intention is to *Really exit <window manager name>*?. If this situation happens and it is still your intention to quit, select the *Yes*, *Really Quit* option. After you have chosen to quit, you are returned to a command-line prompt. Using this method, you will be able to gracefully exit X, which involves stopping all relevant applications and processes in order.

The second method simply involves entering the Ctrl-Alt-Backspace key sequence. Almost immediately, you are returned to a command-line prompt. Alternatively, you could enter Ctrl-Alt-F1, followed by Ctrl-C. But because the two key sequences achieve the same objective as the single-step sequence, you might as well use Ctrl-Alt-Backspace. The single-step method is pretty brutal, though. It stops the *X* server, but then all applications die ungracefully because they simply lose their connections. If you do not want the single-step sequence used on your machine, you can disable it in the `/etc/X11/XF86Config` file.

Meanwhile, if you are in a Desktop environment such as KDE or GNOME, you usually have a Start1xe button in the lower-left corner. If that is the case, all you need to do is click it and select exit or logout or something similar. It is pretty intuitive (now watch me get lost looking for it next time).

# ## Start X Automatically

Before you even think of instituting the following procedure for starting X automatically, you must ensure that your X configuration works properly. Otherwise, you might have trouble logging into your system. To carry out this procedure, you have to be the root user.

# ### Test xdm with the nodaemon Argument

The xdm program (X Display Manager) can control one or more X display sessions on one or more servers, local and remote. This application presents you with what is called an xlogin widget (basically a graphical prompt for a username and password) and then invokes the X Window System after you have been authenticated. You can customize xdm with the