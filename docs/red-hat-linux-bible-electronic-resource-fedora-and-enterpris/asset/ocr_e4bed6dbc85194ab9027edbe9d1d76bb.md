If you are unable to get the video card and monitor configured properly, or if you don't need a GUI, you can configure the computer to start up in text mode. To do this using any shell text editor (such as the vi command described in Chapter 3), change the initdefault line in the /etc/inittab file from id:5:initdefault: to id:3:initdefault:.
If you prefer to have Red Hat Linux boot to a GUI, change the 3 to a 5 instead.

# Tuning your video card and monitor

If your GUI is starting up but needs some tuning (to get better resolution, more colors, or to fix flickering), you can use the Display Settings window to fix your desktop. For the current Red Hat Linux, the Display Settings window was enhanced so that you can use it from a command with no GUI running. The next sections describe how to run the Display Settings window, then how to review the resulting XF86Config file to understand your settings.

# Running the Display Settings window

Red Hat recently replaced the Xconfigurator tool with a new Display Settings window (redhat-config-xfree86 command). This window lets you set the most basic functions relating to your display, monitor, and video card. The Display Settings window is easy-to-use and no longer requires a running X desktop to use it.

To open the Display Settings window from the Red Hat menu, click System Settings → Display. To open that window from a text prompt (even with no GUI running), type **redhat-config-xfree86** (as root). The Display Settings window appears, as shown in Figure 3-20.

From the Display tab, you can try different resolutions (screen width and height in pixels) and color depth (from 256 colors to millions of color). Click the Advanced tab to try to configure your monitor and video card. Click OK to save your changes.

Here are a few tips for using the Display Settings window:

+   - If you know your monitor type, but it is not being detected, click the Advanced tab and then click Configure. You can select the monitor from a list of monitors (by manufacturer) or, if it's not on the list, enter information about the monitor's horizontal and vertical sync rates from the manufacturer's instructions.

+   - If the video card supports 3D hardware acceleration, but is not turned on, you might be able to enable that feature from the Advanced tab under the Video Card section. Just click the Enable Hardware 3D Acceleration check box.