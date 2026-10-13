![](bbox=[0.2, 0.16, 0.28, 0.24])

> Do not use an XF86Config from someone who does not have the same graphics card and monitor as you! Incorrect settings can damage your monitor. Do not use monitor settings outside your monitor's specifications . You have been warned! The only exception to this rule might be for PC notebook users with exactly the same components.

Before you try to start an X11 session using your new XF86Config settings , as the root operator , open the file in your favorite text editor , disable line wrapping , and check the settings. It is essential, especially for laptop users , to do this to check the created settings, enable or disable some X server options , enter the correct amount of video memory , and fine-tune monitor settings.

# The XF86Config Files Section

The Files section tells the X server the location of the color name database and system fonts .

# The XF86Config ServerFlags Section

Several parts of this section can be used to configure special actions enabled by your XFree86 X server . Enable a particular action by removing the pound sign (#) in front of the specific flag. Most users do not disable the DontZap feature because it provides a quick way to exit an X session . The DontZap feature can be disabled if you use X in only one video resolution , such as 800x600 pixels.

# The XF86Config Keyboard Section

The Keyboard section tells the X server what type of keyboard to expect and settings to use, such as language type , key character layout , and manufacturer.

# The XF86Config Pointer Section

The Pointer section tells the X server what pointer, or mouse, to use and how the buttons are handled. Some Protocol settings are Auto for a serial mouse and BusMouse for a bus mouse. The Device entry, /dev/mouse, is a symbolic link to the actual device (such as /dev/ttyS0 for a serial mouse).

![](bbox=[0.18, 0.9, 0.27, 0.96])

> Two-button mouse users definitely want to enable the three-button emulator , in which simultaneously depressing both buttons simulates pressing the middle button, or button 2. One common use of button 2 is to paste text or graphics. For more information about configuring a mouse, see the file README.mouse under the /usr/X11R6/lib/X11/doc directory.