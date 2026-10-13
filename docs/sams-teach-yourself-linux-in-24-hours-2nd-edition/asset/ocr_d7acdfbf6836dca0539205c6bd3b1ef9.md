![](bbox=[0.22, 0.17, 0.28, 0.26])

> This section of your XF86Config file is critical. The device definition is used to tell the X server exactly what type of video chipset and options to support. For a list of device identifiers and options, see the README file under the /usr/X11R6/lib/X11/doc directory corresponding with your chipset.

# The XF86Config Screen Section

The Screen section tells what X server to use, the color depth (such as 8-, 16-, 24- or 32-bits per pixel), screen size (such as 640×480, 800×600, or 1024×768, and so on), and the size of the virtual screen.

This section contains directions for your chosen X server (the XF86_SVGA or other color server, the 4-bit, and 16-color XF86_VGA16 server, or the monochrome server, XF86_Mono) on what resolutions and virtual screen size to support.

For example, if you're using the 8-bit, or 256-color, mode of the XF86_SVGA server, you might have the choice of a 640×480 display (with an 800×600 virtual screen) or an 800×600 display. Resolutions can be toggled during your X session by holding down the Ctrl+Alt keys and depressing the plus (+) or minus (-) keys on your keypad. Laptop users need to use the NumLock key before switching resolutions.

# Bypassing or Disabling the kdm Login Display

The default OpenLinux configuration uses X11 and the kdm client to provide a log-in screen. However, you can bypass this screen and go directly to a log-in prompt for a text-only console (without X11) by pressing Ctrl+Alt+F2. You then see a log-in prompt. To return to the kdm login, press Alt+F1.

Alt+F1 or Alt+F2 are known as virtual consoles. This means that with Linux, you can have up to six different logins from the keyboard of the same computer at the same time. See Hour 7, "Using the X Window System," for details about using virtual consoles and X11.

If you don't want Linux to start X11 or use the kdm graphical login display, you can configure OpenLinux not to use kdm after booting. First, log in as the root operator, and make a copy of the file inittab under the /etc directory with the cp command like this:

```
# cp /etc/inittab /etc/inittab.org
```

Next, use a favorite text editor (discussed in Hour 14, "Text Processing"), open the file, and look for the following line:

```
id:5:initdefault
```