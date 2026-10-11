![](bbox=[0.05, 0.05, 0.95, 0.09])

**Figure 7-6** Application icons in the taskbar

One of the great things about the Linux GUI is that it is very modular. It’s composed of several different pieces that work together to create the graphical interface. Because the GUI is modular, you can mix and match different components together to customize the way it works. This provides a degree of flexibility that just isn’t available with other operating systems. The Linux GUI is composed of the following components:

+   - **X server** The heart of the Linux GUI is the X server software. The X server software is the component that draws windows graphically on the display screen. It’s also responsible for managing your mouse and your keyboard. We call it a *server* because it is capable of displaying output not only on the local monitor, but also on any other system on the network that is also running X server software. The location where the X server software sends its output is controlled by the DISPLAY environment variable.

Over the years, two different X server software packages have been implemented on Linux systems. These include:

+   - **X.org\_X11** X.org is the most commonly implemented X server system and is the default X server used by most modern Linux distributions.

+   - **XF\_ree86** Until about 2004, XF\_ree86 was the default version of X server used by most Linux distributions. It works in pretty much the same manner as X.org. In fact, the development of X.org was based on XF\_ree86. Unfortunately, there were licensing issues associated with XF\_ree86 that drove the Linux community to X.org as an alternative X server.

+   - **Window manager** While X server creates windows within the GUI environment, the window manager’s job is to customize how the windows look and behave. A wide variety of window managers are currently available for Linux. Each one offers a different look and feel for our GUI environment. Some of the more popular window managers include the following:

+   - enlightenment
+   - fvwm
+   - kwin
+   - sawfish
+   - twm
+   - wmaker

Which is best? None is best, really. It all depends on what you like. Some window managers are complex and full featured, such as enlightenment, kwin, and sawfish. In fact, the enlightenment and sawfish window managers are commonly used with the GNOME desktop environment, while the kwin window manager is commonly used with the KDE desktop environment.