
In addition, **shutdown** writes an entry in the system log noting the time of the shutdown and who performed the shutdown.

> **NOTE**
> You need to be the root user to shut down the system—either by logging in directly as root or by using the **su** command to become root.

To shut down your system now, type **su** and press Enter. Then, enter the root password when prompted. If you receive a message complaining that you are not in the proper group to use **su**, log out and then log back in as root. Then, assuming there are no other users logged in to the system, issue the following command:

    shutdown -h now

As mentioned in Chapter 2, on a multiuser system, you would not normally shut down the system like this. Instead, you would give users some warning about the impending shutdown.

After the shutdown has completed, you will see the following message:

    System halted
    Please press any key to reboot

Then, and only then, is it safe to turn off your system.

## Notes on halt and reboot

Two other commands can be used to halt and reboot the system: **halt** and **reboot**, respectively. However, I do not recommend that you get in the habit of using them. Neither of these commands runs the *rc.shutdown* script, which can cause some programs to terminate improperly. Also, neither of these programs allows you to specify a delay, and neither gives users any warning about the impending shutdown. Therefore, you should always use the **shutdown** command to halt the system.

However, these two programs do have their uses. You can use **halt** to make the system 100-percent safe to power down after you have shut down all multiuser processes through the **shutdown** command. The **reboot** command is also handy if you're working in single-user mode; it simply kills all running processes with a **SIGKILL** (a nonignorable signal) and reboots immediately. These commands are helpful for saving time when it's safe to use them, but those occasions are rare.

> **NOTE**
> If you've used DOS and/or Windows in the past, you might be in the habit of using the Ctrl+Alt+Delete combination to reboot a system. By default, FreeBSD will trap the signal sent by this combination and perform the equivalent of running the *reboot* command. This can be a problem when normal users have access to the server's keyboard, because it allows them to reboot the system without being root. In Chapter 10, you will see how to configure FreeBSD to trap the Ctrl+Alt+Delete sequence to prevent it from rebooting the system.

# CHAPTER 5

# Working with
X-Windows

Chapter 4, “Your First Session with FreeBSD,” briefly introduced the X-Windows system. In this chapter, we will look at X-Windows in more detail. The X-Windows system basically has two parts—the X-Server and the window manager. The X-Server runs on your system and provides a graphical framework for applications to use. The window manager determines how X-Windows looks and feels. In this chapter, you learn about these parts of the system in more detail and how to work about and customize the WindowMaker window manager.

## The X-Server

The X-Server is the underlying framework that allows graphical applications to run. By itself, the X-Server is not very useful because it contains no window-management functions. Figure 5.1 shows an X-Server running with no window manager.

Several applications are running in the X-Windows session shown in Figure 5.1: an xterm, a clock, a calculator, and the GIMP image-processing program used to take this screenshot. Notice that the windows have no title bars and borders. They are not resizable or movable, and they cannot be minimized or maximized. Obviously, this lack of flexibility makes for a pretty useless graphical user interface. This is where the window manager comes in.

### IN THIS CHAPTER

- The X-Server
- Windows Managers
- The WindowMaker Window Manager
- Working with Windows
- WindowMaker Menus
- Working with the Dock
- Customizing WindowMaker
- The Preferences Utility

![](img/48eec858cce7dfb89da36a4d40b7daf3_119_0.png)

FIGURE 5.1 Here you see a very bland and rather useless X session.

## Window Managers

The window manager controls how the graphical environment looks and works. Dozens of different window managers are available for X-Windows, so it is almost infinitely customizable. If you don’t like the way X-Windows looks or feels, you can either customize your existing window manager or switch to a completely different window manager.

Figure 5.2 shows the same session as Figure 5.1, but this time it is running under the WindowMaker window manager.

In Figure 5.2 you see that each of the application windows now has a title bar with controls to maximize and close it. In addition, you can resize a window in a window manager interface. On the right side of the desktop is a menu from which you can launch applications by clicking an icon. Right-clicking the mouse on the desktop brings up another menu from which you can select various options or launch applications.

If the WindowMaker desktop isn’t your cup of tea, you can use a different one. Figures 5.3 and 5.4 show just two of the window managers available to you—GNOME and Blackbox, respectively. You learn how to choose an alternative window manager later in this chapter. These figures simply give you an idea how customizable X-Windows is.

![](img/48eec858cce7dfb89da36a4d40b7daf3_120_0.png)

FIGURE 5.2 WindowMaker is a much more useful interface to X-Windows.

![](img/48eec858cce7dfb89da36a4d40b7daf3_120_1.png)

FIGURE 5.3 The GNOME Desktop Environment rivals the Microsoft and Apple desktops’ ease of use and features. However, this desktop also rivals Microsoft’s for heavy resource usage.

![](img/48eec858cce7dfb89da36a4d40b7daf3_121_0.png)

FIGURE 5.4 Blackbox is a no-frills window manager that stays out of the way and uses very few resources. It’s a good choice for servers and older laptops.

This chapter focuses on WindowMaker for a couple reasons. For one, I am adamantly biased toward WindowMaker; it happens to be my favorite X-Windows desktop. But aside from my personal bias, WindowMaker does a good job of balancing ease of use and low resource requirements. Because of this, WindowMaker makes a good desktop for either a workstation or a server. It strikes a middle ground between the easy-to-use-but-resource-gobbling GNOME and the resource-light-but-not-so-easy-to-use Blackbox. (Both GNOME and Blackbox are available in the ports collection under the wm category. See Chapter 14, “Installing Additional Software,” for more information on installing software from the ports collection.)

## The WindowMaker Window Manager

WindowMaker is a clone of the now defunct desktop for the NeXTSTEP operating system. This desktop is perhaps one of the most useful and functional desktops ever designed. Figure 5.5 shows a WindowMaker desktop.

![](img/48eec858cce7dfb89da36a4d40b7daf3_122_0.png)

FIGURE 5.5 The WindowMaker desktop contains a number of easy-to-use features.

The following list describes the main features of the WindowMaker desktop:

- The column of buttons along the right side of the desktop is known as the dock. Although you can't arbitrarily place icons on the WindowMaker desktop like you can in Windows, you can place buttons to launch commonly used applications onto the dock. The main advantage the dock offers over arbitrary icons is that it is never covered up, even when windows are maximized. Therefore, your application buttons are always available. In addition to application launchers, you can also place "mini-programs" on the dock. The calendar/clock shown in the figure is an example of one of these mini-programs. You learn more about the dock in “Working with the Dock,” later in this chapter.
- You can think of the icons for currently running applications as being similar to the Windows taskbar. Double-clicking an icon, for example, will restore a window that has been minimized.
- The Applications menu is similar to the Start menu in Windows. This menu is accessed by right-clicking a blank area of the desktop.
