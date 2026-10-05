
# Introduction and Installation SuSE Linux
PART I

Figure 4.1 SuSE's sax command generates the required XF86 config for XFree86.

![](img/cbac72550c7126a22162e94d91a0c360_103_0.png)

The first dialog box is used to configure X11 to work with your computer's mouse. Choose the appropriate protocol and device for your pointing device. Next, click the Properties tab. You'll see the dialog box shown in Figure 4.2.

Figure 4.2 The Properties dialog box is used to configure your pointer's movement and button sampling rate.

![](img/cbac72550c7126a22162e94d91a0c360_103_1.png)

This dialog box is used to configure the default speed, movement, and button sampling rate for your pointer. Most users will probably use the default values and click the Options tab. These values can be changed later on using the xset command or a KDE pointer configuration dialog box.

After you click Options, you'll see the dialog box shown in Figure 4.3.

# The X Window System
CHAPTER 4

FIGURE 4.3
The sax command's options dialog box is used to select three-button emulation or to set speed options for serial-interface pointers.

![](img/cbac72550c7126a22162e94d91a0c360_104_0.png)

# Note

If you have a two-button mouse, definitely select three-button emulation. Standard pointing devices for X use buttons. Most often the left, or first, button is used to click buttons or window decorations. The middle, or second, button is used to paste copied text or data. The right, or third, button can be used to control scrolling. When you emulate three buttons, a simultaneous depress of the left and right mouse buttons will emulate the middle, or second, mouse button.

When you have finished with your selections, click the Test tab to test your settings. A test dialog box, shown in Figure 4.4, will appear. Move your pointer to the mouse graphic, and then click the left, middle, or right mouse button, and you should see the appropriate button highlighted. This dialog box is also handy to select right- or left-handed pointer operation (although you can reassign pointer buttons with the xmodmap command).

![](img/cbac72550c7126a22162e94d91a0c360_104_1.png)

FIGURE 4.4
The Test dialog box allows you to test your pointer settings and assign right- or left-handed button arrangement.

![](img/cbac72550c7126a22162e94d91a0c360_104_2.png)

The X Window System

# Introduction and Installation suSE Linux
PART I

When you've finish, click the OK button and confirm your settings, as shown in Figure 4.5.

FIGURE 4.5
Confirm pointer settings before moving to the next dialog box.

![](img/cbac72550c7126a22162e94d91a0c360_105_0.png)

If you need to make any changes, click the Expert button. If not, click the Apply button, and then click the Next button to continue. You'll then see the dialog box shown in Figure 4.6.

FIGURE 4.6
The Keyboard dialog box is used to select the keyboard you'll use with XFree.

![](img/cbac72550c7126a22162e94d91a0c360_105_1.png)

# The X Window System
CHAPTER 4

The Keyboard dialog box contains several scrollable lists of information listing various keyboards or languages for keyboards you can use during your X session. Scroll through the lists, and click the desired keyboard and language. If you click in the Test area, you can test various keystrokes from your keyboard. When finished, click the Apply, followed by the Next button. You'll see the Card dialog box shown in Figure 4.7.

FIGURE 4.7
The Card dialog box is used to select your computer's graphics card.

![](img/cbac72550c7126a22162e94d91a0c360_106_0.png)

You can have use the X server to automatically detect your graphics card, or you can scroll through the list of more than 200 cards and select one that corresponds to the one installed in your computer. If you click the Expert button, you'll see the dialog box shown in Figure 4.8, which allows you to choose other options for your graphics card.

FIGURE 4.8
The CardExpert dialog box during card configuration offers additional options you can use to configure X11 to work with your graphics card.

![](img/cbac72550c7126a22162e94d91a0c360_106_1.png)

The X Window System

# Introduction and Installation SuSE Linux
PART I

Click the X server drop-down menu, and scroll through the list of servers until you find one for your graphics card. You can also set the specific amount of video memory available for your card through the Memory list. If you click the Chipsets tab, you can select a specific chipset, and then, after clicking the Options tab, scroll through a list of options for your selected chipset.

Note
Chipset options are specific to a particular chipset. You can read more about the various options available for your graphics card chipset by reading the pertinent README file under the /usr/X11R6/lib/doc directory. Some chipsets have more than two dozen options.

When you've finished your selections, click the OK button, and then the Next button to continue. You'll see a dialog box (see Figure 4.9) used to configure XFree86 for your computer's monitor (note that laptop users will most likely select the LCD monitor).

![](img/cbac72550c7126a22162e94d91a0c360_107_0.png)

Scroll through the list of monitor vendors. When you select a vendor, you'll see a list of models. If you do not see your monitor listed, you can click the Expert button to enter the details manually. When you've finished, click the OK button, and then the Next button to continue. You'll see a dialog box (see Figure 4.9) used to configure XFree86 for your computer's monitor.

# The X Window System
CHAPTER 4

FIGURE 4.10
The Expert dialog box is used to enter horizontal and vertical ranges for your monitor.

![](img/cbac72550c7126a22162e94d91a0c360_108_0.png)

> Caution
Operating your monitor using values out of bounds could result in damage to your hardware.

When finished, click the OK button, and then the Next button. You'll see the Desktop dialog box, as shown in Figure 4.11.

FIGURE 4.11
The Desktop dialog box is used to select the keyboard you'll use with X.

![](img/cbac72550c7126a22162e94d91a0c360_108_1.png)

The X Window System

The dialog box is used to set the maximum size and color depth. You can also select the color depth from the drop-down menu. If you click the Expert button, you'll see the dialog box shown in Figure 4.12, which allows you to choose other options.

FIGURE 4.12
The Expert settings for the Desktop dialog box are used to provide a virtual desktop that is larger than your display.

![](img/cbac72550c7126a22162e94d91a0c360_109_0.png)

# Introduction and Installation SuSE Linux
PART I

The Size and Position controls are used to resize and move the X display. Although many modern monitors offer convenient hardware buttons to stretch, shrink, or move the display, you can do this in software with XFree86 by clicking the appropriate buttons. When you've finished with the current mode, click the Save Mode button. If you defined other modes or resolutions using the Expert dialog box, click the Next or Previous Mode buttons to test or modify each mode. Don't forget to save the settings for each mode.
