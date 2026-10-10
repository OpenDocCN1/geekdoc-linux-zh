# Using Fedora's switchdesk Client

You can use Fedora's switchdesk client to change the default window manager or desktop environment such as GNOME or KDE. Most desktop environments also include the capability to save a session state (such as running applications, the applications' window sizes and positions, and so on), using a feature known as session management.

You can also use the switchdesk utility when running X at a text-based console, along with a keyword (such as GNOME or KDE), to set the default X desktop before launching X. For example, to specify that you want to use the KDE desktop environment as the default, you use switchdesk like this:

```
$ switchdesk KDE
Red Hat Linux switchdesk 4.0
Copyright (C) 1999-2004 Red Hat, Inc
Redistributable under the terms of the GNU General Public License
Desktop now set up to run KDE.
For system defaults, remove /home/andrew/.Xclients
```

This example shows that the default X session will now use KDE. Settings are saving in the file named .Xclients in the home directory. You can launch switchdesk during an X session by clicking the Desktop Switching Tool menu item from the System, Preferences menu. You get a graphical dialog offering a choice of window managers for X sessions (depending on the window managers that are installed on the system), as shown in Figure 3.10.

![](bbox=[0.1, 0.53, 0.5, 0.8])

FIGURE 3.10 You use switchdesk to set the default window manager for X sessions.

Choosing a window manager is a matter of preference, necessity, or policy. You might prefer to use one of the other window managers such as the Tab Window Manager (twm) or Xfce—on legacy PCs because they have lower system resource requirements (that is, they require less hard drive space, CPU horsepower, and system memory). Newer desktop environments require 256MB or even more memory for good performance. The following sections describe some of the most popular window managers and their uses.