I ended this chapter by discussing how to configure accessibility settings on a Linux system. To do this you need to enable Assistive Technologies. One of the tools you can use is called AccessX, which allows you to configure a wide variety of keyboard accessibility settings that enable physically impaired users to use a traditional keyboard:

+   - StickyKeys
+   - MouseKeys
+   - SlowKeys
+   - ToggleKeys
+   - RepeatKeys
+   - BounceKeys
+   - Delay Keys

For physically impaired users who aren't able to use a traditional keyboard, Linux provides the option of using an on-screen keyboard, which allows users to use any pointing device (such as a mouse) to select keys on a virtual keyboard.

In addition to keyboard accessibility, Assistive Technologies also provides mouse accessibility options for physically impaired users. You can configure the following:

+   - Simulated secondary click
+   - Dwell click
+   - Mouse gestures

We next looked at using screen readers to help visually impaired users. Screen readers “read” the text displayed on the screen audibly for the user. The Orca application is probably the most commonly used Linux screen reader. Orca also provides a screen magnifier. A screen magnifier allows visually impaired users to magnify areas of the screen as if they were using a real magnifying glass.

We then looked at using Braille devices with Linux to support visually impaired users. Several types of Braille displays and embossers are supported. To interface with these types of devices, the Linux system must be running the brltty daemon. The Orca application can also be used to interface with Braille devices.

To assist visually impaired users, you can also implement high-contrast, large-text desktop themes.

# ## Accelerated Review

+   - The Linux graphical environment is composed of the following components:
+     - X server
+     - Window manager
+     - Desktop environment
+   - Two different X server software packages have been implemented on Linux systems:
+     - X.org-X11