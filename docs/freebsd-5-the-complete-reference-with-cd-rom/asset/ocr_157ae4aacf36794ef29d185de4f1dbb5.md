video mode, which you can do by clicking the Driver button and clicking the VGA or VESA option. The Fdokey device also works with some cards, but typically with reduced performance. An incorrect choice at this point will cause X to fail at startup.

+   ■ **Monitor** The monitor configuration area lists several common monitor types, such as High Frequency SVGA, 1024x768 @ 70 Hz. If one of these describes your monitor, select it. If you have your monitor's manual, you can use it to locate the precise horizontal and vertical frequency ranges that your monitor accepts and enter those values in the appropriate fields. This will let X take the best advantage of your monitor's capabilities.

> Older monitors can be damaged if run at a higher resolution or refresh rate than their designs permit. Therefore, you should be very careful in entering your monitor information. Do not select a monitor type that supports a higher resolution or refresh rate than you know yours does. Fortunately, most monitors made since the late 1990s ignore out-of-range signals and so can't be damaged by them, but you'll see no display (or a message to the effect that the monitor can't handle the signal) if you try to use such a setting.

+   ■ **Screen** In X configuration parlance, the screen is a specific collection of settings for a video card and monitor. You set the video mode, such as 800x600 or 1280x1024, as a screen. Near the top of the x86cfg display is a bar that reads Configure Layout (see Figure 2-12). Click it and select Configure Screen. A large monitor graphic appears; right click it and pick Configure. You can then add and delete resolutions and color depths to the list on the right; the ones in this list are resolutions that X will attempt to use. As a practical matter, 800x600 is the minimum usable display size for X because many programs assume the display is at least this large. A still better size is 1024x768 if your monitor can handle it. Larger displays are usually better, of course, if your hardware can comfortably accommodate the size.

You can move back and forth between the various options as you see fit, so complete them in whatever order is convenient. When you're finished, click the Quit button at the bottom of the screen. You then have the option to return to configuring or to test your settings. When you're done with all of this, X exits.

# X Desktop Configuration

After configuring XFree86, xinstall lets you configure your X desktop environment. You have several choices:

+   ■ **KDE** The KDE Desktop Environment is one of two major integrated desktop environments that are common on FreeBSD. Most KDE files are missing from