If you don’t know a specific value, use the Probed options. XF86Setup will try to query the card for the unknown information. If your card is unknown, you might want to try the SVGA settings. The system won’t be able to make use of advanced features available for your card, but you’ll be able to work while you find more information about your system.

# Configuring Your Monitor

To begin monitor configuration, select the Monitor button at the top of the display, as shown in the next figure. You’ll need to know the specs for your monitor and supply the appropriate range for horizontal and vertical refresh rates. If you don’t know them, you’ll need to pick one of the options listed. Note that it’s very important that you supply the correct options for your monitor. Using incorrect refresh rates will overdrive your monitor, possibly wrecking it. This is more of an issue with non-multisync-type monitors. If you have your monitor manual, you should enter the settings yourself by hand.

![](bbox=[0.22, 0.46, 0.32, 0.6])

This is the configuration screen for your video card. Note that you can assign multiple settings by clicking the Card List button and picking your card.

Laptop monitors can be especially tricky. Newer laptops might work without problems using standard 640×480, 800×600, or 1024×768 modes. (Select the resolution that matches your laptop’s display.) Some laptops, on the other hand, might exhibit display problems. On my laptop I have been unable to find the proper setting, so when I boot into X-Windows, my screen dances. My fix for a number of years has been to switch between monitor output options (internal and external), and that somehow fixes the problem for the session.

![](bbox=[0.15, 0.89, 0.27, 0.98])

Monitor resolution selects the refresh rates your monitor is capable of supporting. Overclocking a refresh rate will kill a monitor.

# Selecting Resolutions

To begin resolution configuration, select the Modeselection button at the top of the display. You’ll see the screen shown in the next figure. Depending on the amount of video RAM your video card has, it might be possible to specify various resolutions and color settings. By default, X-Windows will use the biggest resolution the card can handle. In some environments, this means enabling a virtual screen in which the screen drops off the right and bottom edges. Moving the cursor to the right or bottom edges scrolls what you see. To me, this sort of setting is disturbing, so I specify settings that match what my monitor can do.