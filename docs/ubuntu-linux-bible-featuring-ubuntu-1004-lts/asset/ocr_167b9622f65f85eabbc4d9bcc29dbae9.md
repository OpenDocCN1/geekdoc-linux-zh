# Chapter 6: Using the Compiz Window Manager

# Other Useful Packages for Compiz

The previous section showed, some extremely useful Compiz-related software is available in the Ubuntu repositories but not installed by default on Ubuntu systems. The previous section discussed the CompizConfig Settings Manager; this section and its subsections discuss some other interesting packages that you can install for use with Compiz (and actually work in any compositing environment, including Xcompmgr).

# Installing and Using the Avant Window Navigator

If you've ever seen or Mac OS X, you're probably familiar with its dock, which is the panelike application at the bottom of the screen (by default), and in when you see for your favorite applications as well as icons representing running applications and the Trash Can. Although Gnome has its Panels and Microsoft Windows its Taskbar, it's hard to deny that the Mac OS Dock is the most active of these entities with similar functionality. Perhaps until now. The Avant Window Navigator (AWN) is an open source dock application for composing window managers that provides an attractive, powerful, extensible, and fully customizable dock for use with Compiz. The Avant Window Navigator was developed by Neil Patel and currently has its home page on the Ubuntu Launchpad site at https://launchpad.net/awn. Figure 6-13 shows the default appearance of an Ubuntu desktop running both the Avant Window Navigator and its configuration utility.

The Avant Window Navigator is not installed by default on Ubuntu systems, but you can easily install it using your favorite package management utility, as explained in Chapter 19. Installing the Avant Window Navigator will also install the library that it uses, some Python modules that it required, and its configuration manager.

**Tip** To get the latest version of the Avant Window Navigator and its plug-ins, you should add http://ppa:launchpad.net/awn-testing/ubuntu to the sources listed in /etc/apt/sources.list. See Chapter 19 for information about enabling other sources for use with Ubuntu's package management system.

After installing AWN, you can start manually from any command-line application, such as xterm or the GNOME Terminal. To configure AWN to start automatically when you log in, you can enable it in the Awn Settings application (discussed later in this) or add it to your standard startup application settings. For the latter, select the System Preferences Startup Applications tools. On the Startup Programs tab, click Add, and enter information about the Avant Window Navigator, as shown in Figure 6-14.