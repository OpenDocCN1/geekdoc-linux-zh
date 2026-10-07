
# Graphics Manipulation 86

- .tif—Tagged Image File Format
- .xbm—X Bitmap image
- .xpm—X Pixmap image, commonly used for Linux icons images

An extensive list of image file extensions can be found in the man page for ImageMagick, an excellent application included with Red Hat, which you learn more about in upcoming sections of this chapter.

> NOTE
> Red Linux includes dozens of graphics conversion programs, and there are few, if any, graphics file formats that can't be manipulated when using Linux. These commands can be used in Perl scripts, shell scripts, or command-line pipes to support many types of complex format conversion and image manipulation. See the manual pages for the ppm, pbm, png, pgm families of commands. Also see the manual page for the convert command, which is part of a suite of extremely capable programs included with the ImageMagick suite.

Often, a file you want to manipulate in one way is in a format that can't be used by either your graphics application or the final application. The solution is to convert the image file, sometimes through several formats. The convert utility from ImageMagick is useful as the netbm family of utilities. If it's not already installed, ImageMagick can be installed with the Packages GUI found in the System Settings menu; the netpbm tools are always installed by default.

The convert utility converts between image formats recognized by ImageMagick. Color depth and size also can be manipulated during the conversion process. You can use ImageMagick to append images, surround them with borders, labels, rotate and shade them, and perform other manipulations well-suited to scripting. Commands associated with ImageMagick include display, animate, and import. The application supports more than 130 different image formats (all listed in the man page for ImageMagick).

The man page for each image format lists conversion utilities; the number of those utilities gives you some indication of the way that format is used:

- The man page for PPM, the portable pixmap file format, lists 32 conversion utilities related to PPM. This makes sense because PPM, or portable pixmap, is considered the lowest common denominator for color image files. Because of this, it's often used as an intermediate format.

- The man page for PGM, the portable graymap file format, lists 11 conversion utilities. This makes sense because PGM is the lowest common denominator for grayscale image files.

- The main page for PNM, the portable anymap file format, lists eight conversion utilities related to it. However, there is no format associated with PNM because it operates in concert with PPM, PGM, and PBM.

- An examination of the main page for PBM, the portable bitmap file format, reveals no conversion utilities. It is a monochrome format and serves as the foundation of other related formats.

## Capturing Screen Images

You can use graphics manipulation tools to capture images that are displayed on your computer screen. Although this technique was used for the production of this book, it has broader uses; truth to the cliché that a picture is worth a thousand words. Sometimes, it is easier to show an example than it is to describe it. A captured screen image (also called a screen grab or a screenshot) can illustrate an error in the display of an application (a font problem, for example) or an error dialog that's too complex to copy down by hand. You might want to share an image of your beautifully crafted custom configuration with your friends or illustrate your written documents. In this section, you learn how to capture screen images for these and other purposes.

When using GNOME desktop, you can take advantage of the built-in screenshot mechanism (gnome-panel-screenshot). Access this tool by pressing the Print Screen key. Captured images are saved in .png format.

> Fun with ImageMagick's identify
> You can use ImageMagick's command to identify details about image files. The welcoming splash of images and the Shadow Man for the GRUB bootloader is located in /boot/grub is a gzipped .xpm image. If you gzip it and run it on it, you'll discover that it is a 640x480 XPM image with 8-bit color depth. That's all you need to know to construct a replacement of image yours. Using the GIMP or other graphics tools, crop or resize your image to 640x480 and change the color to 8 bits. Save it as splash.xpm and then gzip the resulting file. Replace the original Red Hat file and you now have a custom image. The use of identify helped you duplicate parameters of the original image to comply with the requirements of GRUB.

The command is useful to identify unknown image files and to determine whether they're corrupt.

You can also capture screen images from a remote computer using tools supported by Red Hat Linux. The import command (one of ImageMagick's commands) was used to take the screens for this book, for example, using a local computer and a remote computer on a local network.

First we ran xhost + on the remote computer to allow another computer access to the X server on the remote machine; the command to take the screenshot is on our local machine like this

```bash
$ import -window root -display 192.168.168:0 26fig@0
```

This utility made a difficult task easy because the publisher required the screenshots to be done from an 800×600 screen (too small to comfortably work in) and in .pex (IBM Paintbrush) format to accommodate their printing and production equipment.

We could also have used the classic Unix tool xwd to take screenshots. the command would have looked similar to import:

```bash
$ xwd -root -display 192.168.4:0 -out 26fig07.pcx
```

Although the screenshots could have been taken with the GIMP and saved in the appropriate format, we would have to be running the GIMP on that computer and navigating the menus every time we captured an image—the remote option of import was very convenient.

We didn't use Ksnapshot because it doesn't support the .pcx format and it must run locally, but it can take screenshots easily and is our preferred tool for use on a single machine.

## Linux Gaming

Red Linux has three sources of games: the GNOME games, the KDE games, and the X games. All are free and fun.

## Multimedia Applications

Many arcade-style and action games are available for Red Linux. In addition, there are traditional games like solitaire and traditional board games like chess. More sophisticated games are also available for Linux, and Red Hat—with a little help—can be used to play Unreal Tournament 2003.

## Installing Video Drivers

Red Hat does not provide the official NVIDIA drivers because they are closed source. The use of these drivers is controversial in Linux communities because they aren't open source. To the credit of those in Open Source community who might be opposed to them, it's still possible to install these drivers. The following steps assume that you have an NVIDIA card and have already configured it to run XFree86.

You should first obtain the drivers from the NVIDIA site. At this writing, the most current drivers available are version 1.0-3123. You should carefully read the installation instructions. The drivers come in two parts: the GLX code and the kernel driver. I chose to download the RPMs for each and reclaim them on my Red Hat 8.0 system. You'll also find precompiled Binary RPMs that work just as well, but there's no challenge in that.

After it was downloaded, each RPM was recompiled with the following command. (Disregard the RPM commands given in the NVIDIA instructions because they apply to earlier versions of RPM than are provided by Red Hat; the new RPM command separates the building of RPM out of rpm and now places them in rpmbuild).

```bash
# rpmbuild -recompile NVIDIA_kernel-1.0-3123.src.rpm
# rpmbuild -recompile NVIDIA_GLX-1.0-3123.src.rpm
```

After the command is completed, the new RPM files will be found in /usr/src/redhat/rpms/i386. You may install them at the same time with the command:

- rpm -ivh NVIDIA_kernel-1.0-3123.src.rpm
- rpm -ivh NVIDIA_GLX-1.0-3123.src.rpm

You should stop the X server (use #init 3 to change to level 3), and edit the /etc/X11/XFree86Config (make a backup copy of the existing configuration first) to comment out the following lines, if they exist:

```
Load dri
Load GLCore
```
