# The X Window System
CHAPTER 4

# TABLE 4.1 XFree86 Documentation

| File | Description |
| README.cirrus | Information about XFree86 support for Cirrus Logic chipset |
| README.clkprog | Programming information about external video clock setting programs |
| README.cyrix | Info for Cyrix MeigaGX users |
| README.epson | Info for EPSON SPC8110 users |
| README.mouse | Details about XFree86's X11 mouse support |
| README.neo | Info for NeoMagic chipset users |
| README.rendition | Details about Rendition chipset users |
| README.trident | Notes for Trident chipset users |
| README.tseng | Notes for Tseng chipset users |
| RELNOTES | The definitive releases for XFree86 |
| ServersOnly | How your directories should look when building XFree86 X servers |
| VGADriver.Doc | A HOWTO on adding an SVGA or VGA drive to XFree86 |
| VideoModes.doc | Eric S. Raymond's comprehensive treatise on building X86Config models |
| xinput | General information on input device (such as joystick) support in XFree86

If you're new to X11, first read the pages for X and XFree86 for an overview of X. Before configuring, Red Hat should also read the quickstart.doc text. You need to know some technical details about your computer and your computer's video card and monitor. The following is some of the information that will help:

+   * The type, make, name, or model of video card installed in your computer
* How much video RAM (not system RAM) is installed for your card
* The type of clockchip used by your video card chipset
* The type of mouse you use (PS/2 or serial, for example)
* The type, make, or model of monitor attached to your computer
* The vertical and horizontal refresh rates for your monitor (such as 55-100, 30-60 horizontal)
* The type of keyboard you use

Armed with this information, you then have to choose the method or tool for configuring XFree86 and generate a correct XFree86Config file for your system.

You can also manually build your XFree86Config file. The SaX, XFree86Setup and xf86config programs will run from your console's command line or from a terminal window's command line. XFree86's XF86Setup has the advantage of providing a graphical

# 4 The X Window System manual