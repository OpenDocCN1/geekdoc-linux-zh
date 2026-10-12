# The Screen Section

The Screen section ties together the information from the previous sections (using the Screen0, Device, and Monitor Identifier entries). It can also specify one or more color depths and resolutions for the session. Here's an example:

```
Section "Screen"
Identifier "Screen0"
Device "Videocard0"
Monitor "Monitor0"
DefaultDepth 24
SubSection "Display"
Viewport 0 0
Depth 16
Modes "1024x768" "800x600" "640x480"
EndSubSection
EndSection
```

In this example a color depth of thousands of colors and a resolution of 1024×768 is the default, with optional resolutions of 800×600 and 640×480. Multiple Display subsection entries with different color depths and resolutions (with settings such as Depth 24 for millions of colors) can be used if supported by the graphics card and monitor combination. You can also use a DefaultDepth entry (which is 24, or thousands of colors, in the example), along with a specific color depth to standardize display depths in installations.

You can also specify a desktop resolution larger than that supported by the hardware in your monitor or notebook display. This setting is known as a virtual resolution in the Display subsection. This allows, for example, an 800×600 display to pan (that is, slide around inside) a virtual window of 1024×768.

> **NOTE**
> 
> If your monitor and graphics card support multiple resolutions and the settings are properly configured, you can use the key combination of Ctrl+Alt+Keypad+ or Ctrl+Alt+Keypad- to change resolutions on-the-fly during your X session.

# Configuring X

Although the Fedora installer can be used to configure X during installation, problems can arise if the PC's video card is not recognized. If you are unable to configure X during installation (see Chapter 3, “Installing Fedora” ), do not specify booting to a graphical configuration and skip the X configuration portion of the installation. Note that some installs, such as for servers, don't require that X be configured for use in order to support active X sessions but might require installation of X and related software to support remote users and clients.

You can use the following configuration tools, among others, to create a working xorg.conf file: