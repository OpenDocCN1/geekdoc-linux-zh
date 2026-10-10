window. To use this feature, you have to run the **ktalkd** daemon. However, the default Caldera OpenLinux setup does not use the **ktalkd** daemon. If you are interested in setting it up, see the online help by pressing **Help** on the Talk Configuration module.

# Sound

The Sound category lets you control system sounds. The Bell entry lets you set the volume, pitch, and duration of the system beep. Note that not all systems can change the volume or pitch of the beep.

The System Sounds entry lets you associate sounds with various events like opening or closing a window, logging out, and so forth. Whenever you perform an action with a matching sound, the KDE window manager plays the sound. This is fun at first, but it quickly becomes annoying.

# Windows

Finally, the Windows category lets you alter the behavior of KDE windows. You can change things like which buttons appear in the window title bar and which keys work through the list of windows.

This category also lets you change how windows react to mouse clicks. For example, if you want button 2 in the title bar to raise a window instead of button 1, you can configure it to be so.

There are many configuration options in this category, but they are all self-explanatory. Spend a happy few minutes poking around and seeing how you can configure your system.

# Some KDE Applications

Now that I have covered the basics of KDE itself, let’s look at some KDE applications. KDE applications are normal X Window applications that understand the KDE conventions and follow the KDE user interface guidelines. This means that KDE applications can exchange data using drag and drop, they have a consistent user-interface with similar shortcut keys, and they all have a uniform appearance.

# The KDE Package Manager

The KDE package manager is a graphical front end for the RPM software package management system. (RPM is described in detail in Chapter 7.)

To start the KDE package manager, type **kpackage** at the shell prompt. Alternatively, click on an ``.rpm'' file from the file manager. The **kpackage** window appears (Figure 5.9).