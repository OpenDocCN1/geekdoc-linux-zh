# The XFree86 Configuration File

Although you'll probably never have to construct an X configuration file by hand, you do need to know the overall structure, sections, and some of the entries for the exam.

Whatever version it is, the configuration file sets up the server, drivers, input devices, paths for fonts, and other modules. Then it sets up the display parameters, refresh rates, modes, and resolutions.

The older **xf86Config** format is a lot longer and includes many entries that don't change much, if ever. Part of the reorganization was to simplify the overly complex file format. The newer format is much easier to understand and configure manually.

The older **xf86Config** file's sections are listed here with short descriptions:

+   ▶ **Files**—Font paths and color database location
+   ▶ **ServerFlags**—Customization of the X server
+   ▶ **Keyboard**—Keyboard configuration
+   ▶ **Pointer**—Mouse or pointing device configuration
+   ▶ **Monitor**—Monitors and modes configured
+   ▶ **Device**—Video devices (cards)
+   ▶ **Screen**—The resulting combination of a device and the monitor

In contrast, the XF86Config version 4 from Red Hat's Enterprise Linux line contains fewer sections and is representative of the new format. Version 4's sections are listed here, with a short description of each:

+   ▶ **ServerLayout**—This identifies components of the server.
+   ▶ **Files**—This is where you get fonts from, local or remote.
+   ▶ **InputDevice**—Usually two, a keyboard definition and a mouse definition, are included. Others might be included, depending on your hardware.
+   ▶ **Monitor**—This is the horizontal sync, vertical refresh, model name, and so on.
+   ▶ **Device**—This is the video card driver name and RAM amount.
+   ▶ **Screen**—This is the color depth and resolutions for that screen.