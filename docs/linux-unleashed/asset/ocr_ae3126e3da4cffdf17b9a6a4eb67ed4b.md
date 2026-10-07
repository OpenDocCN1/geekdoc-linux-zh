If you don’t have the Hardware HOWTO file or your video card is not listed and you don’t want to use a generic driver, then you must manually configure XFree86. Even if you use the `ConfigXFree` or `xf86config` script to install XFree86, you may still have to make manual modifications to tweak your installation.

Most of the configuration details for XFree86 version 2.X are contained in a file called `Xconfig`, whereas XFree86 version 3.X uses a file called `XF86Config` or `xconfig`, depending on the version. The bare-bones instructions for setting up an `Xconfig` or `XF86Config` file are spread out over several text files included with the XFree86 distribution set. In most cases, you should check the `README`, `VideoModes.doc`, `README.Config`, and `README.Linux` files. That’s not all: You also have to read the man pages for `Xconfig`, `XF86Config` XFree86, and `XFree86bd`. Finally, you should check the man pages for the server version you are running, if one is provided. (It’s a good idea to print out the man pages for easier reference.)

There are a few items of information you need to properly complete the `xconfig` or `FX86Config` file. Before you start configuring XFree86, take a moment to note the following details:

+   • The XFree86 server to be used.
• The type of mouse on your system and the port it is connected to.
• Your video card’s brand name and chipset. If you’re not sure of the chipset, either consult your documentation or use a utility program such as `SuperProbe` (Linux) or `MSD` (DOS).
• Your video monitor brand name and model number, as well as the size of the monitor. It also helps to know the maximum horizontal and vertical scan frequencies, usually available from the monitor’s documentation.
• The type of keyboard you will be using if not the U.S. generic type. Most users have the U.S. type, although some countries have customized keyboards that require different key mappings.

If you don’t know some of the information and don’t have an easy way (such as a utility program) to find out, you should check the documentation that comes with XFree86. Many distributions contain a directory such as `/usr/X11/lib/X11/doc` (usually linked to `/usr/X88/lib/X11/doc` or `/usr/X11R6/lib/X11/doc`) that contains a number of files describing many cards and monitors supported by XFree86 and the essential configuration information (such as monitor scan rates, which are always difficult to determine because you invariably can’t remember where you placed the manual).

When you’ve noted all this configuration information, you are ready to start configuring XFree86. This all begins with the `Xconfig` or `XF86Config` file.