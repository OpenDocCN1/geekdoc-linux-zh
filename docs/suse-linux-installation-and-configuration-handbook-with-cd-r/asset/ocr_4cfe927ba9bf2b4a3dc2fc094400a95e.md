# Starting KDE

Starting KDE on SuSE Linux is very easy. SuSE Linux 6.3 prepares your system to use graphical login using KDM by default. If you log in using KDM, enter your username and password, select KDE as your window manager, and click the Login button. You should log in to KDE immediately.

If you log in to your system using the normal console login, type the following:

```
bash$startx
```

If you have KDE installed, KDE should start immediately because it is the default desktop environment, if it's found on the system. For more information on how to set up graphical login using KDM, refer to Chapter 3, "Installing the X Window System."

# KDE Basics

The first step in KDE is understanding the various parts of it. Your KDE interface consists of the following basic items:

+   - **KWM**—KWM is the KDE window manager. A window manager's importance arises from the fact that the X server does not offer any window decoration. KWM offers much more than decoration. KWM's functions will be discussed in detail in the next sections.
+   - **KPanel**—KPanel is the bar that contains the K button, which is normally used to start KDE applications. It also shows the current running programs to enable easy switching between them.
+   - **KFM**—The current KDE File Manager. KFM serves as file manager, mime-type handler, Web browser, and FTP client. Konquerer in KDE 2.0 will replace KFM.

In fact, although these are the parts you see, there are many other parts of KDE running behind the scenes to serve you. However, you should start by learning about what you can see.

# KWM

KDE can use any KDE-compliant window manager. However, the default window manager that comes with KDE, KWM, works best with it. KWM is responsible for the following jobs:

+   - **Window decorations**—KWM draws the window decorations. Window decorations include the title bar for the windows, the window frames, and the window shape. KWM is themable, which means that you can apply themes to your windows instead of the default KDE theme. SuSE Linux comes with a large collection of KWM themes that can completely change the look of your KDE.