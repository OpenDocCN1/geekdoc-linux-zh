
You will find that Fedora successfully identifies and configures most modern USB-based scanners.

Many scanners are supported in Linux. If yours is not, it still might be possible to use it. The Kooka and Xsane scanner applications are included with Fedora and are fairly straightforward to use. They can both be found in the Graphics menu as the Scanner Tool.

## Working with Graphics Formats

Image file formats are developed to serve a specific technical purpose (lossless compression, for example, where the file size is reduced without sacrificing image quality) or to meet a need for a proprietary format for competitive reasons. Many file formats are covered by one or more patents. For example, the GIF format had fallen into disfavor with the open-source crowd because the patent holder waited a while before deciding to enforce his patent rights.

If you want to view or manipulate an image, you need to identify the file format to choose the proper tool for working with the image. The file's extension is your first indicator of the file's format. The graphics image formats supported by the applications included with Fedora include the following:

- **.bmp** — Bitmaped graphics, commonly used in Microsoft Windows
- **.gif** — CompuServe Graphics Interchange Format
- **.jpg** — Joint Photographic Experts Group
- **.pcx** — IBM Paintbrush
- **.png** — Portable Network Graphics
- **.svg** — Scalable Vector Graphics
- **.tif** — Tagged Image File format

An extensive list of image file extensions can be found in the **man** page for ImageMagick, an excellent application included with Fedora, which you learn more about in upcoming sections of this chapter.

> **TIP**
>
> Fedora includes dozens of graphics conversion programs that are accessible through the command line, and there are few, if any, graphics file formats that cannot be manipulated when using Linux. These programs can be called in Perl scripts, shell scripts, or command-line pipes to support many types of complex format conversion and image manipulation tasks. See the man pages for the **ppm**, **pbm**, **pnm**, and **pbm** families of commands. Also see the man page for the **convert** command, which is part of a suite of extremely capable programs included with the ImageMagick suite.

Often, a file you want to manipulate in some way is in a format that cannot be used by either your graphics application or the final application. The solution is to convert the image file—sometimes through several formats. The *convert* utility from ImageMagick is useful, as is the **netpbm** family of utilities. If it is not already installed, ImageMagick can be installed with the Add Remove Software GUI found in the System Settings menu; the **netpbm** tools are always installed by default.

The *convert* utility converts between image formats recognized by ImageMagick. Color depth and size also can be manipulated during the conversion process. You can use ImageMagick to append images, surround them with borders, add labels, rotate and shade them, and perform other manipulations well suited to scripting. Commands associated with ImageMagick include **display**, **animate**, **identify**, and **import**. The application supports more than 130 different image formats (all listed in the man page for ImageMagick).

## Fun with ImageMagick’s *identify*

You can use ImageMagick's **identify** command to identify details about image files. The welcoming splash image used for the GRUB bootloader is located in /boot/grub and is a **gzipped** .xpm image. If you run **identify** on the image, you’ll discover that it’s a 640×480 xpm image with 16-bit color depth. That’s all you need to know to construct a replacement image of your own. Using The GIMP or another graphics tool, crop or resize your chosen image to 640×480 and change the color depth to 16 bits. Save the image as splash.xpm and then gzip the resulting file. Replace the original Fedora file, and you now have a custom boot image. The use of **identify** helped you duplicate the parameters of the original image to comply with the requirements of GRUB.

The **identify** command is also useful to identify unknown image files and to determine whether they’re corrupt.

The **netpbm** tools are installed by default because they compose the underpinnings of graphics format manipulation. The man page for each image format lists related conversion utilities; the number of those utilities gives you some indication of the way that format is used and shows how one is built on another:

- The man page for **ppm**, the portable pixmap file format, lists 47 conversion utilities related to **ppm**. This makes sense because **ppm**, or **portable pixmap**, is considered the lowest common denominator for color image files. It is therefore often used as an intermediate format.
- The man page for **pgm**, the portable graymap file format, lists 22 conversion utilities. This makes sense because **pgm** is the lowest common denominator for grayscale image files.
- The man page for **pnm**, the portable anymap file format, lists 31 conversion utilities related to it. However, there is no format associated with **pnm** because it operates in concert with **ppm**, **pgm**, and **pbm**.

An examination of the man page for **pbm**, the portable bitmap file format, reveals no conversion utilities. It’s a monochrome format and serves as the foundation of the other related formats.

## Capturing Screen Images

You can use graphics manipulation tools to capture images that are displayed on your computer screen. Although this technique was used for the production of this book, it has broader uses; there is truth to the cliché that a picture is worth a thousand words. Sometimes it is easier to show an example than it is to describe it.

A captured screen image (also called a screen grab or a screenshot) can be used to illustrate an error in the display of an application (a font problem, for example) or an error dialog that is too complex to copy down by hand. You might just want to share an image of your beautifully crafted custom desktop configuration with your friends or illustrate your written documents.

When using the GNOME desktop, you can take advantage of the built-in screenshot mechanism (gnome-panel1-screenshot). Access this tool by pressing the Print Screen key. (Alt+Print Screen takes a screenshot of only the window that has focus on a desktop.) Captured images are saved in .png format.

## Using Digital Cameras with Fedora

Most digital cameras used in connection with Fedora fall into one of two categories: webcams (small, low-resolution cameras connected to the computer’s interface) or hand-held digital cameras that record image data on disks or memory cards for downloading and viewing on a PC. Fedora supports both types. Other types of cameras, such as surveillance cameras that connect directly to a network via wire or wireless connections, need no special support (other than a network connection and viewing software) to be used with a Linux computer.

Fedora supports hundreds of different digital cameras, from early parallel-port (CPIA chipset-based) cameras to today’s USB-based cameras. You can even use Intel’s QX3 USB microscope with Fedora. If you prefer a standalone network-based webcam, explore the capabilities of Linux-based cameras from Axis (at http://www.axis.com/products/video/camera/productguide.htm). The following sections describe some of the more commonly used still camera hardware and software supported by Fedora.

## Handheld Digital Cameras

Digital cameras are one of the major success stories of the last few years. Now you can take pictures and see previews of your pictures immediately. The pictures themselves are stored on disks or memory cards that can be easily plugged into Fedora for further manipulation, using The GIMP or other software. Unfortunately, most of the supplied software that comes with the cameras tend to be for Windows users only, making you reliant on the packages supplied with Fedora.

The good news, though, is that because of the good development carried out in Fedora and GNOME, you are now able to plug pretty much any camera into your computer through a USB interface and Fedora automatically recognizes the camera as a USB mass storage device. You can even set Fedora to recognize when a camera is plugged in so that it automatically imports your photographs for you.

To do this, you need to set up your settings for removable drives and media. You can find this in the System, Preferences, Hardware menu. Click the Cameras tab and select the option to import digital photographs when connected (see Figure 7.6).

![](img/34e72348d53ca54c2a1d9c871316691b_185_0.png)

FIGURE 7.6 Use GNOME’s intelligent handling of removable media by setting it to import your photographs automatically.

Now whenever you connect a digital camera to your computer GNOME automatically detects it (see Figure 7.7), and asks whether you want to import the photographs.

![](img/34e72348d53ca54c2a1d9c871316691b_185_1.png)

FIGURE 7.7 GNOME detects the presence of a digital camera and asks whether the photos should be imported.
