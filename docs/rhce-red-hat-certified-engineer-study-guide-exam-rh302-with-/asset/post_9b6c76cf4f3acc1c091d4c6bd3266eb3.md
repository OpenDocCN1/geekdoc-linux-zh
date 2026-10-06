
640 Chapter 26 · Installing and Configuring X

# FIGURE 26.12 The Xconfigurator 4.3.5 - (C) 2000 Red Hat Software and others

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_649_0.png)

Select one or more desired resolutions and color depths. If you select multiple modes, you can use Ctrl+Alt+pp to cycle them during X operation. However, you must use the + key on the numeric keypad; the ordinary + key will not function for this purpose. When you have selected the desired modes, click the OK button. The Probing to Probing screen, shown in Figure 26.13, will appear.

# FIGURE 26.13 The Xconfigurator Probing to begin

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_649_1.png)

Click the OK button to test your X configuration. If the configuration is a good one, you will see a small dialog box asking "Can you see this message?" If you can see the dialog box, click the Yes button. A second dialog box will ask if you want to configure the system to start X at boot time. Click the Yes or No button, according to your preference.

If you can't see the small dialog box, Xconfigurator will return you to the configuration procedure after several seconds. You can specify different operating parameters and try again to start X.

Laptops are notoriously difficult to configure for X. One reason is that seemingly identical laptops may contain very different hardware. For on-configuring Linux laptops, see the Linux Laptop Web page, www.utexas.edu/users/kharker/linux-laptop.

Now complete Exercise 26.1 to gain experience using Xconfigurator.

EXERCISE 26.1

# Using Xconfigurator

You may sometimes find it necessary to install X after installing Linux. This exercise gives you practice in doing so. Perform these steps:

- 1. Install X and the X-related packages that are required to use Xconfigurator.
2. Configure X by using Xconfigurator. Verify that the configuration works.
3. Configure X by using Xconfigurator's quickstart facility. Verify that the configuration works.

For assistance in completing this exercise, you may refer to this book and other documentation. However, before taking the RHCE exam, be sure you can install X using Xconfigurator without recourse to help.

# XF86Setup

The XFree86 Project distributes its own X configuration tool, XF86Setup. Some administrators prefer the tool to Xconfigurator because it allows use of the mouse. To do so, it uses the facilities of the VGA16 server, which is supported by a wide range of video devices.

To use XF86Setup, you should install the following packages in addition to those in the preceding section:

- glib10, a library of utility functions, which of some are used by the tool
- tcl, a scripting language used by CA
- tk, a widget set used by tcl
- XFree86-VGA16, the VGA16 server
- XFree86-XF86Setup, the tool itself

To install these packages, move to the directory containing them and issue the command

```
rpm -Uvh glib10-*.rpm tcl-*.rpm tk-*.rpm \
XFree86-VGA16-*.rpm XFree86-XF86Setup-*.rpm
```

To launch XF86Setup, use the command

# XF86Setup

The XF86Setup introduction screen, shown in Figure 26.14, will appear.

FIGURE 26.14 The XF86Setup Introduction screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_651_0.png)

The screen provides six buttons around its top:

- The Mouse button lets you configure the mouse.
- The Keyboard button lets you configure the keyboard.
- The Card button lets you configure the video device.
- The Monitor button lets you configure the monitor.
- The Mode Selection button lets you configure the color depths and video resolutions.
- The Other button lets you configure several X options.

To configure the mouse, click the Mouse button. A help screen will appear, explaining various mouse-related options. After you've parsed the information, click Dismiss to close the window. The Mouse screen, shown in Figure 26.15, will appear.

# FIGURE 26.15 The XF86Setup screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_652_0.png)

Select the desired mouse options. Click the Apply button to immediately apply the mouse configuration. When the mouse is working properly, click the Keyboard button. The Keyboard screen, shown in Figure 26.16, will appear.

# FIGURE 26.16 The XF86Setup keyboard screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_653_0.png)

Select the desired keyboard options. Click the Apply button to immediately apply the keyboard configuration. When the keyboard is working properly, click the Card button. The Card screen, shown in Figure 26.17, will appear.

# FIGURE 26.17 The XF86Setup Card screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_654_0.png)

Select the proper card from the list. If the card is not listed, click the Detailed Setup button to enter the configuration manually. The Detailed Card, shown in Figure 26.18, will appear.

# FIGURE 26.18 The XF86Setup Detailed card screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_655_0.png)

Select the proper configuration for the card. If you prefer, you can click the Card List button to return to the Card screen. when the configuration is properly set, click the Monitor button. The Monitor screen, shown in Figure 26.19, will appear.

# FIGURE 26.19 The XF86Setup Monitor screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_656_0.png)

The horizontal sync rate and vertical refresh rate for the monitor. Or, if you prefer, select the list item that corresponds to the characteristics of the monitor. Click the Mode Selection button. The Mode Selection screen, shown in Figure 2.20, will appear.

# FIGURE 26.20 The XF86Setup Mode Selection screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_657_0.png)

Select the color depth you prefer. Select only values supported by the video device. When you've made your selections, click the Other button. The Other screen, shown in 26.21, will appear.

# FIGURE 26.21 The XF86Setup Other screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_658_0.png)

The Other screen lets you enable and disable several X options. When you've selected the configuration, click the Done button. XF86Setup builds the configuration you've specified and stores it in /etc/X11/XF86Config. For more information on XF86Setup, see its page. Now Complete Exercise 26.2 to gain experience with XF86Setup.

EXERCISE 26.2

# Using XF86Setup

The XF86Setup tool gives you greater control over the X configuration than does Xconfigurator. To gain experience using XF86Setup, perform these steps:

- 1. Install X and the X-related packages required to use XF86Setup.
2. Configure X using XF86Setup. Verify that the configuration works.
For assistance in completing this exercise, you may refer to this book and other documentation. However, before taking the RHCE exam, be sure you can install X using XF86Setup without recourse to help.

# xf86config

The third X configuration tool, xf86config, is a text-based tool that uses a prompt/reply dialog to configure X. As such, the tool is somewhat cumbersome to use. But it is highly flexible and is contained in the XFree86 package. Thus, xf86config may work where other tools require installation of additional packages.

The steps in the xf86config dialog resemble those of Xconfigurator and XF86Setup, because all gather essentially the same information. The basic steps are:

- Introduction
- Mouse configuration
- Keyboard configuration
- Monitor configuration
- Card configuration
- Server selection
- Mode selection
- Configuration file generation

Now complete Exercise 26.3 to gain experience using xf86config.

EXERCISE 26.3

# Using xf86config

The xf86config tool has a less sophisticated user interface than Xconfigurator or XF86Setup, but it gives you a great deal of control over the X configuration. To gain experience using xf86config, perform these steps:

- 1. Install X.
2. Configure X using xf86config. Verify that the configuration works.
