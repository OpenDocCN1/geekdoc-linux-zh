# Linux Web Server Toolkit

If you have a high-resolution monitor that goes far beyond 1280 x 1024, you'll probably have to hand-edit the configuration file to get the best results.
If you've directed by the README file for your card (from a button in the Card section), or if you're having problems in general, you can try the options in the Other section. Otherwise, you don't need to even look at that page. Just press the Done button at the bottom of the screen and reconfirm the settings.
X Window System starts up using the settings you've just entered. If you want to see how precise X can be with your video card, choose the option presented to run xvdtime. The xvline utility (shown in Figure 5-13) lets you adjust the exact position of your display on the monitor, centering it vertically and horizontally by adjusting the scan frequencies. If you don't need to do this, or if you have a monitor that has manual controls, you can skip xvdtime. Just choose the button to save the new configuration.

![](bbox=[0.152, 0.365, 0.93, 0.645])

Figure 5-13: The xvdtime utility enables you to set precise frequencies for your screen width, horizontal position, and other similar settings.

The configuration file is written (with your confirmation), a link is created to the X server you've selected, and the XF86Setup utility exits. Now you can start the graphical system at any time by entering the following command:

```
startx
```

When you enter this command, a screen of information appears, followed by a moment by the blue background of X. It may take a moment to finish loading, especially the first time. Eventually, the entire Caldera Desktop will appear, as shown in Figure 5-14.