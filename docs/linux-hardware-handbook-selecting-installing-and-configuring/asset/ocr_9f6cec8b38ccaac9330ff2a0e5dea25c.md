Instead of, or in addition to, running a new X configuration utility, you can edit the xf86config file directly. As created by most configuration utilities, it's well commented, and you can find lines in it corresponding to each of the questions the xf86config configuration tool asked you. You'll also find lines containing modelines—detailed timing specifications for monitors. I discuss modelines in more detail in Chapter 14, “Monitors.”

One modification to XF86Config that you're likely to want to make is to adjust the default color depth. X defaults to using 8-bit color, which is inadequate for most users. Near the end of the XF86Config file, you'll find one or more sections that begin with the keywords Section "Screen". Locate the one with the monitor information you entered into xf86config, and add the following line just before the first display subsection:

```
DefaultColorDepth 16
```

You can change the color depth from 16 to 24 or 32 if you like, but some programs have problems at these depths—particularly at 24. (This problem should be fixed with XFree86 4.0.)

# # Commerc­ial X Servers

In most cases, XFree86 is a perfectly adequate X server for Linux users. There are, however, two commercial X servers that compete with XFree86, and there are times when one of these servers might be desirable.

# ## Commerc­ial X Server Options

The two commercial X servers for Linux are

+   *   **Accelerated-X**	From Xi Graphics (http://www.xig.com), this server is regarded as one of the fastest X servers available for many video cards. Xi Graphics adds support for new video cards somewhat faster than does the XFree86 team. A version of Accelerated-X that supports the OpenGL 3D API is also available. One unusual characteristic of Accelerated-X is that it allows programs to run at bit depths that don't match the screen's actual setting. For instance, Accelerated-X can tell a program that works best at 16 bpp that it's running at that depth when the screen is actually set to 24 bpp or 32 bpp.
+   *   **Metro-X**	This server, from MetroLink (http://www.metrolink.com), is generally not as fast as Accelerated-X. This server is distinguished by its support for touch screens, multi-screen configurations, and 3D input devices.

You can find more information about both these servers, including their supported video cards, on their respective Web sites. A demo version of Accelerated-X is available, so you can test it out on your hardware if you'd like to assess its suitability for your system.