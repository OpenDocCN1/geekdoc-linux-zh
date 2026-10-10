The `X11` primary configuration file is `/etc/X11/xorg.conf`, though it sometimes is stored in the `/etc/` directory. Typically this file is no longer used. Instead, `X11` creates a session configuration on the fly using runtime autodetection of the hardware involved with each GUI's session.

However, in some cases, autodetect might not work properly and you need to make `X11` configuration changes. In those cases, you can create the configuration file. To do this, shut down the X server, open a terminal emulator, and using super user privileges, generate the file via the `xorg -configure` command. The file, named `xorg.conf.new`, will be in your local directory. Make any necessary tweaks, rename the file, move the file to its proper location, and restart the X server.

The `xorg.conf` file has several sections. Each section contains important configuration information as follows:

+   * Input Device: Configures the session's keyboard and mouse
+   * Monitor: Sets the session's monitor configuration
+   * Modes: Defines video modes
+   * Device: Configures the session's video card(s)
+   * Screen: Sets the session's screen resolution and color depth
+   * Module: Denotes any modules that need to be loaded
+   * Files: Set file path names, if needed, for fonts, modules, and keyboard layout files
+   * Server Flags: Configures global X server options
+   * Server Layout: Links together all the session's input and output devices

Keep in mind that many desktop environments also provide dialog boxes in their UI, which allow you to configure your GUI X sessions. Most likely you will have little to no need to ever create or tweak the `X11` configuration file. However, if you want to dig into the `X11` configuration file's details, view its man page by issuing the `man 5 xorg.conf` command.

![](bbox=[0.17, 0.67, 0.25, 0.72])

> While most desktop environments use their own display manager, the X display manager is a basic one available for use. It employs the X Display Manager Control Protocol (XDMCP). The main configuration file is `/etc/X11/xdm/xdm-config`.

If you need to troubleshoot `X` problems, two utilities can help: `xdpyinfo` and `xwininfo`. The `xdpyinfo` command provides information about the X server, including the different screen types available, the default communication parameter values, protocol extension information, and so on.

The `xwininfo` utility is focused on providing window information. If no options are given, an interactive utility asks you to click the window for which you desire statistics. The displayed stats include location information, the window's dimensions (width and height), color map ID, and so on.