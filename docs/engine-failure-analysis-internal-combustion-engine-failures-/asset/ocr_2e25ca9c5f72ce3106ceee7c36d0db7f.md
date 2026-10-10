# **Configuring XFree86**

XFree86 is the default implementation of the X Window System on most Intel-based Linux distributions. Most users should configure XFree86 using configuration utilities, such as **XFree86setup** (see Chapter 1). On Red Hat and Red Hat-derived systems, a utility named **Xconfigurator** is available (see Chapter 1). These utilities considerably ease the difficulty of configuring XFree86 by probing for your system's video hardware and writing the configuration file, XF86Config. However, it is often necessary to modify this configuration file by hand in order to get the desired performance. Accordingly, this system presents the information necessary to modify XF86Config. The still-widely-distributed version 3.3.6 is documented here; see "XF86 Version 4," later in this section, for information on new features and changes. For the latest information on XFree86, including updated versions, visit http://www.xfree86.org.

# **XF86Config: The Overall Structure**

The XF86Config configuration file, XF86Config, is located variously, depending on the distribution you are using. In Red Hat systems, you'll find the file in the /etc/X11 directory, organized into the following sections:

+   * **Files**	Specifies the default paths for fonts and X program modules.
+   * **Module**	Specifies the modules (if any) to be loaded when the X server starts.
+   * **ServerFlags**	Specifies certain server options.
+   * **Keyboard**	Defines the default keyboard configuration for your system.
+   * **Pointer**	Defines the default mouse configuration for your system.
+   * **Monitor**	Defines the default monitor configuration for your system.
+   * **Device**	Defines the video adapter configuration for your system.
+   * **Screen**	Specifies one or more video display modes that are possible with the video adapter that you are using.
+   * **Xinput**	Defines certain input devices, such as joysticks and graphics tablets. This section is optional.