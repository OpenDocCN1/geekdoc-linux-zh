# CONFIGURING THE X SERVER 233

If you specify excessively high values for VertRefresh or HorizSync, you risk the premature demise of your monitor! XFree86 uses these values to exclude from the very beginning those graphic modes that might not be compatible with your monitor.

![](bbox=[0.198, 0.185, 0.833, 0.533])

Figure 7.2 Monitor setup with XF86Setup.

# Terminating the configuration

In the fifth step of XF86setup, the menu item OTHER, you can without problems adopt the default settings. If you subsequently click on DONE, the server is started with your settings. If everything goes well, your monitor will display a stable image. You can now decide via a mouse click whether you want to store the settings, further optimize the image position with xhtune (see page 234), or leave the program with QUIT.

If, in contrast, the monitor is not capable to synchronize after the start of X, there are two alternatives: one is the key combination Alt+Ctrl Ctrl+, where the key of the numeric keypad is used; this allows you to change to a lower-resolution graphics mode. If that does not help, you need to abort the configuration program with Alt+(Ctrl)+(Backspace), restart, and repeat the whole configuration step by step.