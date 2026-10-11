
## X Server Configuration Sections

This section configures the X server with the input devices it should use.
- **InputDevice**
- **Modes** This section defines video modes the X server may use.
- **Screen** This section binds your video board to your monitor.
- **Monitor** This section defines parameters for the monitor connected to your display adapter.
- **ServerLayout** This section glues all of the preceding sections together into a complete configuration.

I pointed out that you should avoid directly editing your X server configuration file. Instead, you should use a configuration utility to avoid mistakes that could potentially damage your hardware. Depending on your distribution, you can use one of the following utilities:

- YaST
- SaX2
- system-config-display
- system-config-keyboard
- system-config-mouse
- xorgconfig or xorgcfg
- Xorg -configure
- XFree-86 -configure
- xf86config or xf86cfg
- xvidtune

To specify your default window manager, you need to edit a hidden configuration file in your user's home directory. The name of the file depends on your distribution and your default runlevel:

- .xinitrc (runlevel 3)
- .Xsession (runlevel 5)
- .Xdefaults (runlevel 5)
- .Xclients (runlevel 5)

You can also set the value of the WINDOWMANAGER environment variable to the desktop environment you want to use.

I next discussed how to configure an X font server. An X font server allows you to configure fonts for an entire organization from a single central location. The first thing you need to do is install the fonts you want to share on the X font server. I discussed the difference between bitmap fonts and scalable fonts. I then discussed where to install the fonts:

- **Type 1** /usr/share/fonts/Type1
- **TrueType** /usr/share/fonts/truetype

After copying the font files to the appropriate directory, you next need to run the mfktfonts and mkfontdir commands to create a font description file and index the font. Then you need to open port 7100 in the X server host’s firewall. The next thing you need to do is tell the X font service (xfs) that the fonts are there and should be made available to remote X server clients by editing the /etc/X11/fs/config file. In this file, you need to remark out the no-listen tcp line and then verify that the appropriate font path is listed under catalogue =.

Once done, you need to start the xfs daemon and configure it to start each time the system boots. Then restart your X server.

At this point, I discussed how to configure the remote X servers to consume the fonts provided by the X font server. This is done by adding a new FontPath directive to the files section of the xorg.conf file that points to the X font server using the following syntax:

```
FontPath "tcp/server_address:7100"
```

I then discussed how you go about configuring your display manager. You can enable or disable the display manager using the xdm init script in the init script directory. You can use the chkconfig command to enable or disable the init script at system boot. You can configure the display manager by editing the appropriate configuration file:

- **xdm** /etc/X11/xdm/xdm-config
- **kdm** The KDE display manager is actually based on xdm and usually uses the xdm configuration files. However, some distributions store kdm settings in /etc/kde/kdm or /etc/X11/kdm instead.
- **gdm** /etc/X11/gdm

You can also use the other files in the /etc/X11/xdm directory to customize the behavior of the xdm display manager:

- **Xresources** Customizes the login interface presented to the user by the display manager after the system has booted
- **Xservers** Changes the default color depth for the display manager

I then discussed how you can configure remote access to the local display manager. First, you need to allow remote access to your display manager. How this is done depends on your distribution and the display manager in use. If your host is running xdm or kdm, edit the /etc/X11/xdm/Xservers file, find the line that begins with :0, and remove the –nolisten tcp option. If your system is running gdm, edit the /etc/X11/gdm/gdm.conf file and set DisallowTCP= to false. If you are running openSUSE, edit the /etc/sysconfig/displaymanager file and make the following changes:

```
DISPLAYMANAGER_REMOTE_ACCESS="yes"
DISPLAYMANAGER_XSERVER_TCP_PORT_6000_OPEN="yes"
```

Then open port 177 in the xdm host’s firewall. Once done, you next open the /etc/X11/xdm/Xaccess file on the xdm host in a text editor and add an entry for each remote system that will access the xdm service on the host.

I ended this chapter by discussing how to configure accessibility settings on a Linux system. To do this you need to enable Assistive Technologies. One of the tools you can use is called AccessX, which allows you to configure a wide variety of keyboard accessibility settings that enable physically impaired users to use a traditional keyboard:

- StickyKeys
- MouseKeys
- SlowKeys
- ToggleKeys
- RepeatKeys
- BounceKeys
- Delay Keys

For physically impaired users who aren't able to use a traditional keyboard, Linux provides the option of using an on-screen keyboard, which allows users to use any pointing device (such as a mouse) to select keys on a virtual keyboard.

In addition to keyboard accessibility, Assistive Technologies also provides mouse accessibility options for physically impaired users. You can configure the following:

- Simulated secondary click
- Dwell click
- Mouse gestures

We next looked at using screen readers to help visually impaired users. Screen readers “read” the text displayed on the screen audibly for the user. The Orca application is probably the most commonly used Linux screen reader. Orca also provides a screen magnifier. A screen magnifier allows visually impaired users to magnify areas of the screen as if they were using a real magnifying glass.

We then looked at using Braille devices with Linux to support visually impaired users. Several types of Braille displays and embossers are supported. To interface with these types of devices, the Linux system must be running the brltty daemon. The Orca application can also be used to interface with Braille devices.

To assist visually impaired users, you can also implement high-contrast, large-text desktop themes.

## Accelerated Review

- The Linux graphical environment is composed of the following components:
  - X server
  - Window manager
  - Desktop environment
- Two different X server software packages have been implemented on Linux systems:
  - X.org-X11
  - XFree86
- Some of the more popular window managers include the following:
  - enlightenment
  - fvwm
  - kwin
  - sawfish
  - twm
  - wmaker
- Two desktop environments are predominantly used with Linux systems today:
  - KDE
  - GNOME
- Before implementing a video board/monitor combination with Linux, you need to check the HCL for your distribution and make sure your video board and monitor are supported.
- Your X configuration is stored in a text file in the `/etc` directory:
  - XFree86 `/etc/X11/XF86Config`
  - X.org `/etc/X11/xorg.conf`
- The `xorg.conf` file is broken into sections that begin with the `Section` directive and end with `EndSection`.
- The most commonly used sections in a typical `xorg.conf` include:
  - `Files` Tells the X server where to find the files it needs to do its job
  - `ServerFlags` Specifies global X server options
  - `Module` Tells the X server to load certain server extension and font rasterizer modules at startup
  - `InputDevice` Configures the X server with the input devices it should use
  - `Modes` Defines video modes the X server may use
  - `Screen` Binds your video board to your monitor
  - `Monitor` Defines parameters for the monitor connected to your display adapter
  - `ServerLayout` Glues all of the preceding sections together into a complete configuration
- You should use a configuration utility to configure your X server software to avoid mistakes that could potentially damage your hardware.
- You can use one of the following utilities to configure your X server software:
  - YaST
  - SaX2
  - system-config-display
