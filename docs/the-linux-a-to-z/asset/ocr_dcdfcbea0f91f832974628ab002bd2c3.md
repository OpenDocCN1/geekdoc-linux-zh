been done by the installation script, but, if not, you can perform the link operation manually, with the command:

```
ln -sf /usr/X11R6/bin/XF86_SVGA /usr/X11R6/bin/X
```

If at any time you need to change the X-server you are using, then this operation will need to be performed again, but with the new server name inserted in the command line as appropriate.

# 10.2 X-configuration

Once you have selected an X-server, the next task is to configure it. This is done by creating the configuration file:

```
/etc/XF86Config
```

Before you even think about doing this, let me first warn you that it is possible to create a configuration file that can drive your display monitor outside its operating specification. If you do this, there is every chance that you could cause permanent damage to your monitor. For this reason, please exercise the utmost caution when setting up the XF86Config file.

The configuration file itself consists of several sections of information about various aspects of your hardware layout. These sections are:

+   - **files** Specifies the pathnames of the RGB database and the various X-windows character font files.
- **server flags** Used to specify some X-server options.
- **keyboard** Gives keyboard attributes, such as keyboard protocol, auto key repeat characteristics, and num-lock behavior.
- **pointer** Specifies what type of mouse X should look for, what device special file is being used for the mouse, and then such things as baud rate for serial mice and whether or not to emulate the third button on a two-button mouse.
- **monitor** Allows you specify display monitor characteristics such as bandwidth, horizontal sync and vertical refresh frequencies (straight from the monitor manual), as well as giving a list of video modes suitable for use with the monitor.
- **device** This section allows you to specify the technical detail on your video graphics card. If you don’t specify all the necessary values in this section, the X-server can often probe the hardware and discover the missing items for itself.
- **screen** This section specifies which video card, monitor and X-server combination will be used.

The manual page for XF86Config is particularly useful in creating this file along with the contents of the file: