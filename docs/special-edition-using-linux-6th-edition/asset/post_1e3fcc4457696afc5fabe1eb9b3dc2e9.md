
You need about 50–65MB of disk space to install the XFree86 system and the X applications provided (depending on distribution and how many optional components you install). You need at least 16MB of virtual memory to run XFree86. *Virtual memory* is the combination of the physical RAM on your system and the amount of swap space you’ve allocated for Linux. You must have at least 4MB of physical RAM to run XFree86 under Linux, thus requiring a 12MB swap file. The more physical RAM you have, the better the performance of your XFree86 system will be.

Next, you need a video card containing a video-driver chipset supported by XFree86. See http://www.xfree86.org/4.0.1/Status.html for an up-to-date list of all the supported chipsets. Table 5.1 lists a summary of chipset support in XFree86 4.0.1. Note that although many vendors are unsupported in 4.0.1, the most common chipsets generally are supported. Also, if you see a comment such as “most are supported,” you should look at the previously listed Web page for a detailed explanation.

**Table 5.1. Chipset Support in XFree86 4.0.1**

| Manufacturer | Comments |
|---|---|
| 3Dfx | Support for Voodoo 1 and Voodoo 2 through glide driver. Accelerated support for Voodoo Banshee and Voodoo 3 through tdfx driver. |
| 3Dlabs | Accelerated support through glint driver. |
| Alliance | Support for the AT24, AT25 and AT3D through apm driver. Only incomplete support for the AP6422. |
| ARK Logic | No support in 4.0.1. Use 3.3.6. |
| ATI | Accelerated support for the Rage 128 chips through the r128 driver. Accelerated support for the Mach64 Rage variants through the ati driver. Unaccelerated support for all of the others except the Mach8 and some early Mach32 chips through the ati driver. |
| Avance Logic | No support in 4.0.1. Use 3.3.6. |
| Chips & Tech | Accelerated support through the chips driver. |
| Cirrus Logic | Accelerated support for the Alpine and Laguna through the cirrus driver. For other chips, you will need to use 3.3.6. |
| Compaq | No support, use 3.3.6. |
| Cyrix | Spotty support. Use 3.3.6 unless you want to help test the 4.0.1 drivers. |
| DEC | Accelerated support through the tga driver. |
| Epson | No support, use 3.3.6. |
| Genoa | No support, use 3.3.6. |
| IBM | Support for the standard IBM VGA chip (and compatibles) through the vga driver. No support for IBM 8514/A or XGA-2. Use 3.3.6. |
| IIT | No support, use 3.3.6. |
| Intel | Accelerated support for the Intel i740 through the i740 driver. Support for the Intel i810 through the i810 driver. |
| Matrox | Accelerated support through the mga driver. Matrox is somewhat of a standard in the XFree86 world, and these cards tend to be very well tested and supported. |
| MX | No support, use 3.3.6. |
| NCR | No support, use 3.3.6. |
| NeoMagic | Accelerated support through the neomagic driver. |
| NVIDIA | Accelerated support through the nv driver. |
| Number Nine | No support, use 3.3.6. |
| Oak | No support, use 3.3.6. |
| Paradise | No support, use 3.3.6. |
| RealTek | No support, use 3.3.6. |
| Rendition | Support through the rendition driver. |
| S3 | Support for the ViRGE and Trio3D chipsets through the s3virge driver. Other chipsets are only supported in 3.3.6. |
| SiS | Accelerated support for most chips through the sis driver. Some chips’ support is still experimental. |
| Silicon Motion | No support, use 3.3.6. |
| Trident | Accelerated (if applicable) support for most chips through the trident driver. |
| Tseng Labs | Support through the tseng driver. |
| Video 7 | No support. Use 3.3.6. |
| Weitek | No support. Use 3.3.6. |

## INSTALLING FROM RPMS

On RPM-based systems, XFree86 is split into a large number of RPMs; some are required whereas others are optional. If you installed XFree86 when you installed Red Hat or OpenLinux, everything was probably done for you. If you didn’t install XFree86 at that time, or if you’re trying to upgrade XFree86, then you need to decide what packages to install. See Table 5.2 for the list of recommended packages and Table 5.3 for the optional packages that ship with OpenLinux eDesktop. Red Hat RPMs have very similar names for the most common packages.

**Table 5.2. Recommended XFree86 RPMs**

| RPM | Description |
|---|---|
| `XFree86` | Base XFree86 system. |
| `XFree86-config` | XFree86 configuration files. |
| `XFree86-contrib` | Many useful X applications. |
| `XFree86-fonts` | Standard X fonts. |
| `XFree86-libs` | Shared libraries for most X applications. |
| `XFree86-programs` | Core X11 applications. |
| `XFree86-server` | XFree86 server (including all modules). |
| `XFree86-setup` | Configuration utility. On Red Hat, you should install Xconfigurator instead. |

**Table 5.3. Optional XFree86 RPMs**

| RPM | Description |
|---|---|
| `XFree86-addons` | Miscellaneous demos, converters, and minor utilities. |
| `XFree86-config-eg` | Example configuration files for XFree86. |
| `XFree86-devel-*` | Development package. It is required if you plan to develop or compile X applications or servers. `-prof` and `-static` versions of this RPM are available for profiling and static linking, respectively. |
| `XFree86-fonts-*` | Various additional fonts. |
| `XFree86-fontserver` | Font server for XFree86. It is used to provide the fonts on your machine to other machines on the network. |
| `XFree86-imake` | Imake tools required if you want to compile X11 from sources. |
| `XFree86-misc` | Even more miscellaneous programs. |
| `XFree86-twm` | Basic window manager. |
| `XFree86-xdm` | Basic login manager (usually kdm or gdm is used instead). |
| `XFree86-Xnest` | A nested X server. This X server can run in a window under another X server, generally for testing purposes. |
| `XFree86-Xprt` | Print extensions to support output to hardcopy devices using X drawing requests. |
| `XFree86-xsm` | Basic session manager (this will usually be handled by KDE or GNOME). |
| `XFree86-xterm` | Terminal emulator. If you install KDE or GNOME, you won't need this one. |
| `XFree86-Xvfb` | X server that does not require display hardware. It is very useful for development and can also be useful to rendering engines, but generally not used by end users. |

Font packages often come in several flavors. The base version (as listed in Table 5.3) is generally terminal fonts and keyboard re-maps for the languages in question. The 75dpi fonts version contains 75dpi (dots per inch) fonts, which can be used by most monitors. The 100dpi fonts version contains 100dpi fonts, which are good for high-end (usually large) monitors that can handle 100dpi. Finally, some fonts come in a scale version, which are Type 1 scalable fonts. Installing at least the base, 75dpi, and scale versions is highly recommended. If your monitor can support the 100dpi versions, having them can be quite nice as well.

Remember that you have to install the appropriate programs from each package. Although not all packages are required, if you install XFree86 after installing Linux, you should review the full details on the packages to install. If you have the 65MB needed for a full installation, you may want to simply install all of the packages.

You can get the RPMs you want to install either from your distribution’s media or from their Web site. Because various distributions often configure XFree86 in different ways, it is recommended that you choose RPMs specific to your distribution. In particular, your initialization scripts can expect the X server and login manager to be in specific locations. Although most distributions agree that this is /etc/X11, many subtle differences exist in exactly where things are located under that tree.

After you have the RPMs, you can generally install them easily using rpm:

```
# rpm -i XFree86-*.rpm
```

In most cases, this should handle everything, but if you have trouble, consult Chapter 16, “Software Package Management.”

## INSTALLING FROM deb PACKAGES

Debian does not have supported XFree86 4.0.1 packages at the time of this writing. However, test packages are available. Add the following to your /etc/apt/sources.list, and run dselect normally:

```
deb http://samosa.debian.org/~branden/ woody/i386/
```

Select the `xfree86-common` package. This should automatically select most of the other packages you need. Table 5.4 lists the recommended deb packages, and Table 5.5 lists the optional packages.

**Table 5.4. Recommended XFree86 deb Packages**

| Package | Description |
|---|---|
| `xfree86-common` | Base XFree86 system. Get this first. |
| `xbase-clients` | Basic applications. |
| `xf86setup` | XFree86 configuration utility. |
| `xfonts-75dpi` | 75dpi fonts. |
| `xfonts-base` | Basic fonts. |
| `xfonts-scalable` | Type 1 scalable fonts. |
| `xfree86-server` | XFree86 X server. |
| `xfree86-server-common` | XFree86 server infrastructure. |
| `xlib6g` | Xlib libraries (needed by all X11 applications). |
