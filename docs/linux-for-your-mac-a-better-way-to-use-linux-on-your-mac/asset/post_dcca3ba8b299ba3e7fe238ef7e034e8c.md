
## and sizes.

In the recent past, scanners typically used legacy I/O ports on Intel-based and Macintosh computers, such as RS-232 (serial), IEEE-1284 (parallel port), and SCSI. Early digital cameras typically used serial I/O to transfer images. This was a slow, tedious process, generally circumvented by using removable Compact Flash or Smart Media devices.

Today, many scanners, cameras, and printers use the Universal Serial Bus (USB) port. Before you buy a USB scanner, however, check to make sure there is a supporting driver for Linux! Some scanners are supported by the USB scanner kernel module, while others require a stand-alone application in order to acquire documents. One great place to check before you buy is [http://www.linux-usb.org](http://www.linux-usb.org), which lists the status of many drivers, along with user feedback on how well the drivers work.

Along with a driver, you will also need a client that provides either a command-line interface or a graphical interface with traditional controls, such as previewing, cropping, contrast, brightness, or color adjustment. In this arrangement, the driver is known as a back end, while the client is known as the front end. The most popular Linux back-end and front-end software used for many scanners (and some cameras) is SANE (Scanner Access Now Easy) software, discussed next.

### Using SANE

SANE consists of a set of software libraries, configuration files, and one or more command-line or X front-end clients. These will include `xscanimage`, `xscan` (for cameras), and `saned` (which supports scanning over a network). The libraries and clients should be installed from your distribution's CD-ROM.

SANE's device configuration files will be found under the `/etc/sane.d` or `/usr/local/etc/sane.d` directories. The configuration directory contains individual files for each supported device. For example, the Epson family of scanners will use the file `epson.conf`. This file contains settings that tell SANE what type of scanning system is used, and the proper device to poll when attempting a scan. If you have a USB Epson scanner, the entry will be:

```
usb /dev/usbscanner
```

Before attempting to use your scanner, make sure that you have properly configured SANE for your system's setup and scanner model. After configuration, SANE's `xscanimage` client can then be used as a GIMP plug-in or a stand-alone program. `xscanimage`'s settings are stored in resource files under a directory named `xscanimage` in a directory `.sane` in your home directory. The settings files are `xscanimage.rc` (user preferences); `devicename.rc` (driver settings); and `preview.devicename.ppm` (the current saved preview image). Note that you do not have to edit these files at all; they will be saved when setting preferences when you run the scanning client.

To use `xscanimage` as a stand-alone program start it from the command line, like this:

```
$ xscanimage &
```

Insert a document in your scanner and press Enter. When the main window appears, click the Preview Window button, and then click the Acquire Preview button as shown in Figure 13.4.

After the image is previewed, click and drag to crop the portion of the image you wish to scan, then click the Scan button. Use the different controls, buttons, and menus to set the type of scan, resolution, brightness, and contrast.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_325_0.png)

**Figure 13.4** *The xscanimage client offers convenient controls and an image preview window.*

To use `xscanimage` as a GIMP plug-in, navigate to the `~/.gimp/plug-ins` directory in your home directory, and use the `ln` command to create a symbolic link named `xscanimage` that points to the binary version, like this:

```
$ cd .gimp*/plug-ins
$ whereis xscanimage
xscanimage: /usr/local/bin/xscanimage
$ ln -s /usr/local/bin/xscanimage .
```

You can then start the GIMP and use its Xtns menu's Acquire image menu item, as shown in Figure 13.5.

Scan your image using `xscanimage`’s controls. After the image has been previewed and scanned, it will appear in a GIMP editing window, as shown in Figure 13.6.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_326_0.png)

**Figure 13.5** *Use the GIMP Xtns menu’s Acquire image menu to launch the xscanimage client.*

![](img/1ea833f5a3e3c1547e3dd2891f52804a_326_1.png)

**Figure 13.6** *xscanimage will scan directly into a GIMP editing window.*

### Using gPhoto

gPhoto is a versatile and capable digital camera client included with most Linux distributions. You can use this client to download and edit images from your digital camera. If you have a digital camera, chances are gPhoto supports it, because more than 100 cameras (at last count) work with the client.

You can start gPhoto from the command line of an X11 terminal window, like this:

```
$ gphoto &
```

After you press Enter, click the **Configure** menu, then select the **Select Port/Camera model** menu item. You will see a dialog box, as shown in Figure 13.7.

Select the proper port, then click and scroll through the list of cameras to select your particular model. Click the **Save** button when finished.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_327_0.png)

> If you have a serial camera, but want to upload your images to a PowerPC, use a USB-to-serial converter, such as DLink’s PDA adapter. You will need to load the proper usb-serial kernel modules, and then specify the serial port as `/dev/ttyUSB0`.

Use gPhoto to download **thumbnail**, or index, images from your digital camera. Thumbnails are small versions of larger images stored in your camera or on your camera’s removable media. Use the **Camera** menu to select **Download Index**, and then click the **Thumbnails** menu item.

gPhoto also recognizes keyboard shortcuts (like most GNOME-aware clients). Press Ctrl-i to download a thumbnail index of your camera’s contents. The index will then be displayed in gPhoto’s main window, as shown in Figure 13.8.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_327_1.png)

![](img/1ea833f5a3e3c1547e3dd2891f52804a_328_0.png)

**Figure 13.8** Use a thumbnail index for clicking on pictures you would like to download from your camera.

Click on each desired image, and then use the Camera menu to download the pictures. The selected pictures will be displayed in a tabbed window, as shown in Figure 13.9.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_328_1.png)

**Figure 13.9** gPhoto makes the task of quickly editing digital images easy.

You can then perform basic image editing by using gPhoto's toolbar buttons. When you have finished, save each image (the default format is .jpg).

### Converting Graphics

Linux systems use and include many different types of graphics files. The type of most graphics will be recognized by filename extension, such as .gif, .tiff, or .jpg. Other formats include PostScript (.ps), and legacy UNIX graphics, such as .bmp, .png, or .xwd. You will find nearly 50,000 graphics (many in the form of icons) installed on your system following a full install of SuSE PPC Linux.

Mac OS artists will be happy to know that Linux provides a number of capable graphics clients and utilities that may be used to translate or convert familiar graphics files. Some programs, such as the shareware `xv` client, must be used during an X session, while others such as ImageMagick's `convert` command may be used at the text console without an active X session.

A number of Linux graphics commands may be used to flip, rotate, invert, or even crop images. Many others can be used in a shell pipe on the command line. This allows you to combine effects to translate as well as edit batches of images. For example, to convert a Graphics Interchange Format file to Portable Anymap, make the image larger, then convert the image to color Tagged File Format. Create a shell pipe, like this:

```
gi ftpixmap lux.gif | pnmscale -xsize 400 | pnm_smooth | pnmto tiff > lux.tiff
```

In this example, the .gif file is converted to .ppm, then enlarged. The enlarged output is then smoothed, converted to .tiff, and saved as a new graphic. Economy of scale is achieved even more when you must convert entire directories of graphics or wholesale numbers of files.

One of the most capable graphics conversion commands included with Linux is the `convert` command, which can import and export at least 75 different graphics file formats. This command is easy to use, because translation occurs according to filename extension. For example, to convert the new .tiff file back to .gif, use `convert`, like this:

```
# convert lux.tiff lux.gif
```

The `convert` command may also be used for a variety of other effects, such as scaling and cropping (see its manual page for more information).
