**Linux identification tools** The `dmesg` utility, described earlier, may provide clues as to the video card chipset. You can also type `lspci` at a command prompt to obtain identifying information on most of your installed hardware devices, including the video card. Both methods require you to wade through information on nonvideo devices.

One point to keep in mind when identifying the video card chipset is that video cards and video card chipsets are often made by different manufacturers. For instance, nVidia produces chipsets that are used in boards made by ASUS, Biostar, Gigabyte, and others. Linux and X don’t care about who made the video card; only the chipset manufacturer is important.

![](bbox=[0.18, 0.33, 0.28, 0.37])

> NOTE
> Increasingly, video functions are built into computer motherboards. Nonetheless, it’s still common to refer to “video cards” as if they were physically distinct cards, as they once universally were.

# ## Choosing an X Server

All major Linux distributions ship with a free X server. In the past, a server known as XFree86 was common, but most distributions have switched to X.org-X11 instead, because of changes to the XFree86 licensing terms. These two servers are very similar, though; X.org-X11 6.7.0 was based on XFree86 4.3.99. You can learn more about XFree86 at <http://www.xfree86.org>, and X.org-X11 is headquartered at <http://www.x.org>. As I write, the current versions are XFree86 4.8.0 and X.org-X11 7.4.

Linux distributions from 2001 and before used XFree86 3.3.6 or earlier, but more recent distributions use XFree86 4.x or X.org-X11. Some major architectural modifications marked the change to XFree86 4.x, and some configuration files changed with this release. By the time X.org-X11 was forked off the XFree86 project, XFree86 3.3 had become largely obsolete. Thus, I don’t cover this old version of XFree86. If you encounter it or must use it because of poor support for an obscure video card in more recent X servers, though, you should be aware that some configuration options changed between XFree86 3.3.6 and 4.0.

Some video card and chipset manufacturers have made XFree86- and X.org-X11-compatible drivers available for their products. Thus, it’s worth checking the Web sites maintained by your board and chipset manufacturers to see if drivers are available. This is definitely true if the main XFree86 or X.org-X11 release doesn’t include appropriate drivers, and it may be true even if there are drivers—the manufacturers’ offerings often offer improved performance, particularly in the realms of 3D and full-motion video acceleration.

XFree86 or X.org-X11 occasionally doesn’t support a device at all. You have three choices in this case:

Use the frame buffer device. The Linux kernel has some video drivers of its own. These can be accessed via the `frame buffer` X driver. For this to work, your kernel must include frame buffer support for your video chipset.