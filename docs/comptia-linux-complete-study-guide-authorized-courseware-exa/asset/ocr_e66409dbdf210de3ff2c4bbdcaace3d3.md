![](bbox=[0.15, 0.1, 0.35, 0.25])

Major modern desktop OSs all provide some form of *graphical user environment* (GUI), which provides the windows, menus, dialog boxes, flexible fonts, and so on, with which you’re probably familiar. In Linux, the main GUI is known as the *X Window System* (or *X* for short). *X* configuration is either very easy or moderately hard; most distributions today provide auto-detection and easy configuration options during installation, and these usually work correctly. When they don’t, or when you want to tweak the configuration, you must delve into the *X* configuration file or use a GUI *X* configuration tool. Doing either requires that you know how *X* treats the video hardware, among other things.

Beyond basic *X* configuration are a few extra topics. These include fonts, GUI login tools, user desktop environments, using *X* for remote access, and localization. Each of these topics is closely associated with basic *X* configuration, but they all go beyond it in one way or another, extending *X*s capabilities or providing more features for users, as described in this chapter.

The *X* display can be considered one form of output. Another is printing, and this chapter covers that topic, as well. With a properly configured printer, you can obtain hardcopy of the documents you create and edit using both *X* and text-based applications.

# # Configuring Basic X Features

Basic *X* configuration sets features such as the mouse used, the keyboard layout, the screen resolution, the video refresh rate, the display color depth, and the video card you’re using. Some of these options require telling *X* about what hardware you have installed, whereas others enable you to adjust settings on your hardware. In any event, before you proceed with actual configuration, you should know something about the *X* servers that are available for Linux because your selection will determine what additional tools are available and what files you may need to adjust manually. GUI and text-mode configuration utilities can help you configure *X*; but sometimes you must delve into the configuration files, so knowing their format is important. This requires that you know what the major option groups do so you can adjust them.

# ## X Server Options for Linux

Although *X* is by far the dominant GUI for Linux, several implementations of *X* are available:

+   *   **XFree86**  The dominant *X* server in Linux until 2004 was *XFree86* ([http://www.xfree86.org](http://www.xfree86.org)). This open-source server supports a wide array of video cards and input devices, and