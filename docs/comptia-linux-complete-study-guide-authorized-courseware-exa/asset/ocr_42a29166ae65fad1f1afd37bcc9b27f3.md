Another option for running X programs remotely is to use the Virtual Network Com-puting (VNC) system (http://www.realvnc.com). VNC runs a special X server on the computer that’s to be used from a distance, and a special VNC client runs on the computer at which you sit. You use the client to directly contact the server. This reversal of client and server roles over the normal state of affairs with conventional X remote access is beneficial in some situations, such as when you’re trying to access a distant system from behind certain types of firewall. VNC is also a cross-platform protocol; it’s possible to control a Windows or Mac OS system from Linux using VNC, but this isn’t possible with X. (X servers for Windows and Mac OS are available, allowing you to control a Linux system from these non-Linux OSs.)

# # X Accessibility

Historically, most computers have been designed for individuals with normal physical capabilities. As computers have become everyday tools, though, the need for people with various disabilities to use computers has risen. Linux provides tools to help with this task. Some basic X settings (controlled in xorg.conf or XF86Config) can help in this respect—for instance, you can adjust the keyboard repeat rate to prevent spurious key repeats for individuals who may keep keys pressed longer than average. Other settings are unusual and may require the use of unique accessibility tools to set. Some options must be set in specific desktop environments (KDE or GNOME, for example).

# ## Keyboard and Mouse Accessibility Issues

You can set many keyboard and mouse options using ordinary desktop environment tools for personalizing keyboard and mouse responses. Other options are more exotic, such as onscreen keyboards.

![](bbox=[0.15, 0.7, 0.22, 0.77])

> The Linux+ objectives mention AccessX; however, this package as such appears to be abandoned, and its functionality has been folded into the standard desktop environment control panels described in the following pages.

# ## Standard Keyboard and Mouse Options

Most Linux desktop environments include keyboard and mouse control panel options. For instance, in a standard Fedora 12 GNOME installation, you can find these options by selecting System  Preferences  Mouse and System  Preferences  Keyboard. Figure 6.3 shows the Keyboard Preferences control panel. Because the locations of such options can be customized from one distribution to another and can change from one release to another, you may need to hunt for the options in your menus.