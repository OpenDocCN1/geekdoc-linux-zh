
Many scanners are supported in Linux. If yours is not, it still might be possible to use it. The Kooka and Xsane scanner applications are included with Fedora Core Linux, and are covered in detail in Chapter 9, "Productivity Applications." They can be found in the Graphics menu as the Scanning and Scan & OCR Program menu items.

### USB Scanner Success Is Elusive

Because a failure is sometimes more educational than a success, for previous editions of this book, we attempted to configure a USB scanner that wasn't supported: the Canon N650U. With the release of the version of SANE included with Fedora, the scanner is now supported, and is automatically detected!

However, here are the manual steps we used for detecting and configuring this scanner in Linux when it did not work properly:

First, connect the scanner. For this USB scanner, look at the output of:

```
# cat /proc/bus/usb/devices/
```

(We have truncated the output here to show only the scanner. You can also use the `lsusb` command.)

```
T:  Bus=01 Lev=01 Prnt=01 Port=00 Cnt=01 Dev#=  2 Spd=12  MxCh=
D:  Ver= 1.00 Cls=00(>ifc ) Sub=00 Prot=00 MxPS= 8 #Cfgs=   1
P:  Vendor=04a9 ProdID=2206 Rev= 1.00
S:  Manufacturer=Canon
S:  Product=CanoSCon
C:* #Ifs= 1 Cfg#= 1 Atr=80 MxPwr=500mA
I:  If#= 0 Alt= 0 #EPS= 3 Cls=ff(vend.) Sub=00 Prot=ff Driver=(none)
E:  Ad=81(I) Atr=03(Int.) MxPS=   1 Ivl=16ms
E:  Ad=82(I) Atr=02(Bulk) MxPS=  64 Ivl=0ms
E:  Ad=03(0) Atr=02(Bulk) MxPS=  64 Ivl=0ms
```

`Driver=(none)` at the end of the seventh line tells us that the device was not found in the lookup table. Because we now have the "magic" vendor ID and device ID, we can attempt to load the driver manually with

```
# /sbin/modprobe scanner vendor=0x04a9 product=0x2206
```

Now the output of the `cat`/`lsusb` command from before tells us that the scanner device driver is associated with our scanner:

```
I:  If#= 0 Alt= 0 #EPS= 3 Cls=ff(vend.) Sub=00 Prot=ff Driver=usbscanner
```

and the Kooka and Xsane applications now recognize the scanner.

### Graphics Manipulation

If you have ever wished you could change a photograph slightly—red eyes returned to their normal color, dark areas lightened, funny Uncle Bert removed—and longed for a way to accomplish that task, you have been granted your wish. Now, you can accomplish all of these tasks with the tools provided with Fedora (and a digital image from a digital camera or from a scanner).

This section of the chapter discusses The GIMP, a powerful graphics manipulation tool. (You learned about the other graphics tools that Fedora provides in Chapter 9.) In this section of the chapter, you also learn about graphic file formats supported by Fedora, as well as some tools you can use to convert them if the application you want to use requires a different format.

### The GNU Image Manipulation Program

One of the best graphics clients is The GIMP. The GIMP is a free, GPLed image editor with sophisticated capabilities that can import and export more than 30 different graphics formats, including files created with Adobe Photoshop. It is often compared with Photoshop, and The GIMP represents one of the GNU Projects’ first significant successes. You will see many images in Linux that have been prepared with The GIMP.

The GIMP can be started by clicking a desktop panel menu item or by using the command line, like this:

```
$ gimp &
```

You will see an installation dialog box when The GIMP is started for the first time, and then a series of dialog boxes that display information regarding the creation and contents of a local GIMP directory. This directory can contain personal settings, preferences, external application resource files, temporary files, and symbolic links to external software tools used by the editor.

![](img/774d40fd20903495c5cd00e2efad3f33_318_0.png)

Although The GIMP is powerful, it does lack two features Adobe Photoshop offers that are important to some graphics professionals.

The first of these is the ability to generate color separations for commercial press printers (CMYK for the cyan, magenta, yellow, key, or black colors). The GIMP uses RGB (red, green, and blue) which is great for video display, not so great for printing presses. The second feature GIMP lacks is the use of Pantone colors (a patented color specification) to ensure accurate color matching.

If these features are important to you, The GIMP is an excellent tool. If you must use Adobe Photoshop, the current version of CodeWeaver’s Crossover Office will run Photoshop in Linux.

These deficiencies might not last long. A CMYK plugin is in the works, and the Pantone issues will likely be addressed in the near future as well.

After the initial configuration has finished, The GIMP’s main windows and toolboxes appear. The GIMP’s main window contains tools used for selection, drawing, movement, view enlargement or reduction, airbrushing, painting, smudging, copying, filling, and color selection. Depending on the version installed on your system, the toolbox can host more than 25 different tools.

The toolbox's File, Xtns, and Help menus are used for file operations (including the ability to send the current image by electronic mail), image acquisition or manipulation, and documentation, respectively. If you right-click an open image window, you'll see the wealth of The GIMP's menus, as shown in Figure 10.5.

![](img/774d40fd20903495c5cd00e2efad3f33_319_0.png)

FIGURE 10.5 Right-click on an image window to access The GIMP's cascading menus.

### Working with Graphics Formats

Image file formats are developed to serve a specific technical purpose (lossless compression, for example, where the file size is reduced without sacrificing image quality) or to meet a need for a proprietary format for competitive reasons. Many file formats are covered by one or more patents. For example, the GIF format has fallen into disfavor with the open-source crowd because the patent holder has only recently decided to begin enforcing his patent rights.

If you want to view or manipulate an image, you need to identify the file format in order to choose the right tool for working with the image. The file's extension is your first indicator of the file's format. The graphics image formats supported by the applications included with Red Hat include:

- .bmp—Bitmapmed graphics, commonly used in Microsoft Windows
- .cgm—Computer graphics metafile
- .g3—CCITT Group 3 FAX image
- .gif—CompuServe Graphics Interchange Format
- .ico—Microsoft Windows icon image
- .jpg—Joint Photographic Experts Group
- .mng—Multiple-image Network Graphic image
- .pbm—Portable Bitmap File Format
- .pcx—IBM Paintbrush
- .pgm—Portable Graymap File Format
- .png—Portable Network Graphics
- .pnm—Portable Anymap
- .ppm—Portable Pixmap File Format
- .rgb—Raw red, green, and blue samples
- .rs—Sun raster image
- .svg—Scalable Vector Graphics
- .tif—Tagged Image File Format
- .xbm—X bitmap image
- .xpm—X Pixmap image, commonly used for Linux icons images

An extensive list of image file extensions can be found in the man page for ImageMagick, an excellent application included with Fedora, which you learn more about in upcoming sections of this chapter.

> **TIP**
>
> Fedora includes dozens of graphics conversion programs, and there are few, if any, graphics file formats that cannot be manipulated when using Linux. These commands can be used in Perl scripts, shell scripts, or command-line pipes to support many types of complex format conversion and image manipulation tasks. See the manual pages for the ppm, pbm, pnm, and pgm families of commands. Also see the man page for the convert command, which is part of a suite of extremely capable programs included with the ImageMagick suite.

Often, a file you want to manipulate in some way is in a format that cannot be used by either your graphics application or the final application. The solution is to convert the image file—sometimes through several formats. The convert utility from ImageMagick is useful as are the netpbm family of utilities. If it is not already installed, ImageMagick can be installed with the Add Remove Software GUI found in the System Settings menu; the netpbm tools are always installed by default.

The convert utility converts between image formats recognized by ImageMagick. Color depth and size also can be manipulated during the conversion process. You can use ImageMagick to append images, surround them with borders, labels, rotate and shade
