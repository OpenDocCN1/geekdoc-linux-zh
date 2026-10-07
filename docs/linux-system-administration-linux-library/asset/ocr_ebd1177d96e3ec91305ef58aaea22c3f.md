# Chapter 16 The X Window System

manager to launch important utilities from its built-in menus, file manager, and any other tools you want to start the window manager, and open at all times when you log in. The result is typically a much less integrated environment than what you get with a conventional desktop environment, but it may be to your liking. Chances this approach will consume less memory than with a conventional desktop environment, too.

Even if you use a distribution that favors one desktop environment, you can use another. With most distributions, doing so is merely a matter of installing the environment from the distribution's CD-ROM and selecting it from a menu on the XDM login screen. In the event that the XDM does not provide this feature (as the original XDM doesn't), you can start the environment by placing an appropriate command in the \.xssession or equivalent file. For instance, to start KDE, the command is startkde; for GNOME, it's gome-session. It's possible for one user of the system to use one desktop environment and for somebody to use another.

# Mixing Desktop Environment Components

Although most desktop environments come with a wide array of utilities that integrate with one another to a greater or lesser extent, it's usually not necessary to run these tools within their parent environments. You can run KDE's ksCD-ROM player from within GNOME, for instance—or you're not running any desktop environment at all. You can use this fact to your advantage, picking the best parts of each environment. The drawback is that to your advantage, mixing components in this way reduces their interoperability. Programs from two environments might not share a common address-book file, for example, whereas two matched programs share this file.

One further drawback to mixing components in this way, or to keeping two or more environments for the convenience of your users, is that the disk-space requirements can be substantial. Each environment is likely to consume hundreds of megabytes of disk space, although you might be able to get by less for a very minimal installation. If you want to use just a handful of components, you may be able to install them in just a few megabytes.

# X Applications

X applications use X to display information and accept input from the user. They rely on the window manager that the user selects and the widget set that the programmer selects. In some cases, applications share settings or can interact with desktop environments. Usually, though, X applications don't rely on desktop environments.