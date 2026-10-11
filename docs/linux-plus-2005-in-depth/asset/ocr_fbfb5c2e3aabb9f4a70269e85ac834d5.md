After configuring X Windows, you can fine-tune the vsync and hsync of the video card using the **xvidtune** utility after X Windows has started. Simply open a BASH shell in the GUI and type `xvidtune` to start the utility, as shown in Figure 9-23.

![](bbox=[0.15, 0.2, 0.75, 0.46])

Although most monitors today support a wide range of hsync and vsync values, choosing too high of a value for either might damage the monitor. In addition, choosing an hsync or vsync value that is too low might result in headaches over time because the human eye can see lower refresh rates.

A wide variety of X Windows configuration utilities are available in addition to those discussed in this section. These configuration utilities are listed in Table 9-5 and are available depending on the version of X.org or XFree86 as well as the distribution used.

Table 9-5 Common X Windows configuration utilities

| Command | Description |
| :--- | :--- |
| Xorg -configure | When run by the root user, hardware information is automatically detected and written to an X.org configuration file called /root/xorg.conf.new. You must copy this file to the /etc/X11 directory and rename it to xorg.conf for it to be used. |
| XFree86 -configure | When run by the root user, hardware information is automatically detected and written to an XFree86 configuration file called /root/XF86Config.new. You must copy this file to the /etc/X11 directory and rename it to XF86Config for it to be used. |
| XF86Setup | A text-based XFree86 configuration utility included with older versions of XFree86. |