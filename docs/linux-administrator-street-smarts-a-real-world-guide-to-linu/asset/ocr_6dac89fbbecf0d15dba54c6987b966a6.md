# ## Procedure

The X configuration file, like most Linux configuration files, is a text-mode file with options you can alter in a text editor. Before making real changes, you should familiarize yourself with some fundamental X principles and with the basic structure of the configuration file. After that, you can go on to change your mouse, monitor, and video card configurations for the hardware you've installed (or just examine these options if you're not actually changed your hardware).

# ## X Basics

X is Linux's GUI environment. Like most other Linux tools, X is a separate software component that can be replaced with workalike software and that's configured independently of many other subsystems. Traditionally, XFree86 (http://www.xfree86.org) has been the most popular X server for Linux; however, most Linux distributions now use X.org-X11 (http://www.x.org) instead.

Technically, X is a server, much like a file server or mail server. Where a file server enables programs to read and write files, though, X enables programs to read from the keyboard and write to the screen. X's server nature gives it certain unusual networking capabilities, some of which are described shortly, in Task 2.9, “Manage X Logins.”

To configure X, you edit the X configuration file, which goes by various names. For XFree86, the configuration file is called XF86Config or XF86Config-4 and is located in /etc/X11 or /etc. For X.org-X11, the configuration file is xorg.conf, which is normally stored in /etc/X11. The configuration files for X.org-X11 and XFree86 4.x are identical in format. Before proceeding further, you should change to the /etc/X11 directory (or possibly just /etc), back up the configuration file, and then load the original into your favorite text-mode editor. (Task 1.5 in Phase 1 describes using Vi for this purpose.)

# ## Familiarizing Yourself with the Configuration File

The X server configuration file is broken down into multi-line sections, one section for each major feature (mouse, keyboard, video card, and so on). Each of these sections begins with a line consisting of the keyword **Section** and the section name in quotes. Each section ends with the keyword **EndSection**.

```
```
Section 'InputDevice'
  Identifier 'Keyboard0'
  Driver 'kbd'
  Option 'XkbModel' 'pc105'
  Option 'XkbLayout' 'us'
  Option 'AutoRepeat' '500 200'
EndSection
```
```

This section tells X about the keyboard—its model, layout, and so on. If you examine your X configuration file, you'll find several sections:

**Files** This section tells X where to find files that it needs. In many cases, this section consists of nothing but FontPath entries, which tell X where to find fonts. X font configuration is actually