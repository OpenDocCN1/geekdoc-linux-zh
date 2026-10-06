# 84 Part I: Getting Started in Fedora RHEL

This chapter takes you on a tour of your desktop —— going through the process of logging in, trying out some features, and customizing how your desktop looks and behaves. Sections on KDE, GNOME, and Xfce contain reference information on how to set preferences, run applications, configure, and work with the file managers. The last section describes how to use the Settings window to configure your video card and monitor, or if they were not properly detected.

Newer desktop features described in this chapter include the GNOME Desktop and AIGLX desktop effects. Using Online Desktop, you can organize and easily connect to your friends and accounts with Flickr, Amazon, Netflix, Facebook, Mugshot, and many others. With AIGLX, you can get interesting desktop effects, such as windows that wobble when you move them or change workspaces on a revolving cube.

# Logging in to Fedora or RHEL

Because Linux was created as a multiuser system, you start by logging in (even if you are the only person using the computer). Logging accomplishes three functions:

+   * It identifies you as a particular user.
* It starts up your shell and desktop (icons, panels, backgrounds, and so on) configurations.
* It gives you appropriate permissions to change files and run programs.

After the computer has been turned on and the operating system has started, you see either a graphical login screen (default) or a text-based login prompt. The text-based prompt should look something like this:

```
Fedora release 10
Kernel 2.6.27 on an i686

localhost login:
```

> NOTE: If you see a text-based login instead of the graphical login screen, and you want to use the GUI, type your username and password. Then when you use a command prompt, type startx to start up your desktop.

The graphical login is typically your entry into the graphical user interface (GUI). For the current Fedora, the login screen is enabled for Face Browsing. This means that user accounts you add on the login screen, so you can click one to log in as that user. Users can also add an image (96x96 pixels) to represent themselves in the About Me window (select System -> Preferences -> Personal -> About Me to add your own image).

Figure 3-1 shows the middle of the graphical login screen, with a single user selected.