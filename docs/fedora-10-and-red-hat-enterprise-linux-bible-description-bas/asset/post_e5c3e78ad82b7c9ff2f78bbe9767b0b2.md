
# Part I: Getting Started in Fedora RHEL

If you just want to change your desktop environment temporarily, you can select Session from the login screen and choose the desktop you want. You can choose it just for the current session or to have it as your default desktop.

# Using the KDE Desktop

The KDE desktop was developed to provide an interface to Linux and other Microsoft UNIX systems that could compete with Mac OS or Windows operating systems for ease of use. Integrated within KDE are tools for managing files, windows, multiple desktops, and applications. If you can work a mouse, you can learn to navigate the KDE desktop. Fedora 10 includes version 4.1 of KDE.

> NOTE: KDE is not installed by default for Fedora. Therefore, to use the procedures in this section, you might have to install KDE. During installation, you could use a Custom install to install KDE. Otherwise, see Chapter 5 for information on how to use PackageKit or yum to add KDE. You can also try the KDE 4.1 Live CD that comes with this, and even install it to your hard disk.

The lack of an integrated, standardized desktop environment in the past has held Linux and other UNIX systems from acceptance on the desktop. While individual applications could run well, you rarely could drag and drop other items between applications. Likewise, you couldn't open a file and expect the machine to launch the correct application to deal with or save your works from one session to the next. KDE provides a platform for developers to create programs that easily share information and detect how to deal with different data types.

The following section describes how to get started with KDE. This includes the KDE Setup wizard, maneuvering around the desktop, managing files, windows, virtual desktops, and adding application launchers.

# New Features in KDE 4.1

KDE 4 marked some major innovations for the KDE desktop. New libraries were added to support multimedia applications and improving handling of removable devices. There were many applications for viewing documents (such as Okular) and managing files (such as Dolphin). The most important new feature, however, is the Plasma desktop shell.

As with most major software release, there were some bugs in KDE 4. Many of these bugs have been shaken out with the KDE 4.1 desktop included in the latest release of Fedora.

The Plasma desktop shell gives the KDE 4.1 desktop a new look and feel. It features improved ways of finding and presenting information, such as KRunner and KickOff. The new Plasma Panel can incorporate lots of new applets, as well as clocks, pagers, and other useful applications.

Elements in the Plasma desktop shell are referred to as plasmoids. What makes plasmoids differ from components on many of today's desktop systems is that they can be combined in various ways to interact with each other and can be placed in different locations. For example, a particular widget (such as a clock or a news ticker) is important to you, instead of having it represented by a tiny icon on the panel, you can put a big version of the apple upon your desktop.

Descriptions of these and other KDE 4.1 features are included in the following section.

# Starting with KDE

You can select the KDE desktop from the login screen (provided that KDE is installed). Select your login name and choose Session → KDE. Type your password, as prompted. A KDE desktop should appear, similar to the one shown in Figure 3-18.

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_164_0.png)

Figure 3-18: Manage files and applications graphically with the KDE desktop.

# KDE desktop basics

Here are some descriptions of what you will find on the KDE 4.1 Plasma desktop for Fedora 10, as illustrated in Figure 3-18:

- **Plasmoids** — Applets that can be added to the desktop as well as the panel are referred to as plasmoids in KDE 4.1. Here you can see the clock, picture frame, KGet, downloader, network ticker, and dictionary all to the desktop. You can drag plasmoids around, group them, and arrange them as you like on your desktop.
- **Konqueror** — The default Web browser and file manager for KDE.
- **Dolphin** — A new file manager for KDE.
- **Panel** — The panel provides some quick tools for launching applications and managing the desktop. You can adapt the panel to your needs by resizing it, adding tools, and changing its location. By default, you start with an application launcher, taskbar, desktop pager, some mini apps, device modifier, and a clock.
- **Application Launcher/Menu** — This button opens the Kickoff Application menu, which helps you search for applications installed on your system and launch them. Choose between Favorites (applications you use), Applications (application menus), Computer (places and storage devices), or Recently Used Applications. Right-click the select and Switch to Classic Style to return to a classic view of application categories and menus.
- **Taskbar** — This button shows the tasks that are currently running on the desktop. The button for the window that is currently active pressed in. Click a task to toggle between opening and minimizing the window.
- **Desktop Pager** — This box on the panel consists of your virtual desktops, which contain small views of each desktop. There are labeled 1, 2, 3, 4. You join your KDE session on virtual desktop 1. If there are windows on the desktop, small icons representing them may cover the desktop number. You can change to any of the four desktops by clicking it.
- **Mini apps** — Some applications, such as media players, clipboards, and power managers, will keep running after you closed the window. This maintain the apps they represent.
- **Clock** — The current time is shown on the right-hand side of the panel. Click it to see a calendar for the current month. Click the arrow keys on the calendar to move forward and back to months.

# Chapter 3: Getting Started with the Desktop

# Getting around the desktop

Navigating the desktop is done with your mouse and keyboard. You can use a two-button or three-button mouse. Using the keyboard to navigate requires some Alt and Ctrl sequences.

# Using the mouse

The responses from the desktop to your mouse depend on which button you press and where the mouse pointer is. Table 3-2 shows the results of clicking each mouse button with the mouse pointer placed in different locations.

The mouse actions in the table are all single-click. Use single-click with the left mouse button to open an icon on the desktop. On a window title bar, double-clicking results in a window-shade action, the window scrolls up and down into the title bar.

# Table 3-2: Mouse Actions

| Pointer Position | Mouse Button | Results |
|---|---|---|
| Window bar or frame (current window active) | Left | Raise current window. |
| Window bar or frame (current window active) | Middle | Lower current window. |
| Window bar or frame (current window active) | Right | Open operations menu. |
| Window bar or frame (current window not active) | Left | Activate current window and raise it to the top. |
| Window bar or frame (current window not active) | Middle | Activate current window and lower it. |
| Window bar or frame (current window not active) | Right | Open operations menu without changing position. |
| Inner window (current window not active) | Left | Activate current window, raise it to the top, and pass the click to the window. |
| Inner window (current window not active) | Middle | Activate current window and pass the click to the window. |
| Inner window (current window not active) | Right | Activate current window and pass the click to the window. |
| Any part of a window | Middle (plus hold Alt key) | Toggle between raising and lowering the window. |
| Any part of a window | Right (plus hold Alt key) | Resize the window. |
| On the desktop area | Left (hold and drag) | Select a group of icons. |
| On the desktop area | Right | Open system pop-up menu. |
