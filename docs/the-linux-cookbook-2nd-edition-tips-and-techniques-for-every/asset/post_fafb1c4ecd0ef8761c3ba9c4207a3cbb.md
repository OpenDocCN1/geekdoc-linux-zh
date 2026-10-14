
Screenshots taken of virtual consoles, as shown in this recipe, are saved as text files; you can't take screen shots of virtual consoles when graphics are displayed.

## 19.2 Scanning Images

SANE
DEB: sane
RPM: sane
WWW: http://www.sane-project.org/

SANE, “Scanner Access Now Easy,” is the de facto Linux scanner interface; use it to scan an image with a scanner and save it to a file.

SANE works with a wide array of scanning hardware, but make sure the scanning hardware you want to use is compatible by checking for it in the Linux Hardware Compatibility HOWTO [http://en.tldp.org/HOWTO/Hardware-HOWTO/] and in SANE's own list of supported scanners [http://www.sane-project.org/sane-backends.html].

Once you have SANE running, you can scan images with SANE-aware applications like the GIMP (see Recipe 18.3 [Using the GIMP], page 434).

The following recipes describe the use of the command line scanimage tool that comes with the SANE package.

NOTES: As the acronym implies, getting a scanner to work on a Linux system hasn't always been smooth going. The SANE interface is completely open, and its developers are making sure that it is generalized enough to be implementable on any hardware or operating system.

### 19.2.1 Listing Available Scanner Devices

Before you can use a scanner, you need to know its device name. To get this name, use scanimage with the --list-devices option.

⇒ To list available scanner devices, type:

```
$ scanimage --list-devices [RET]
device `umax:/dev/sgb' is a UMAX Astra 1220S flatbed scanner
$
```

In this example, there’s one scanning device on this system, a UMAX brand scanner that can be specified to scanimage by giving its device name, umax:/dev/sgb, as an argument to the -d option.

To list the available resolutions and actions supported by a particular device, use the --help option along with the -d option followed by the device name.

- ⇒ To list available options supported by the device listed in the previous example, type:
- $ scanimage --help -d 'umax:/dev/sgb' [RET]

NOTES: For all scanimage commands, specify the scanner device you want to use by including the -d option with the device name.

### 19.2.2 Testing a Scanner

To run diagnostic tests on a scanner to make sure that it can be properly read from, use scanimage with the --test option.

- ⇒ To test the UMAX scanner listed previously, type:
- $ scanimage --test -d 'umax:/dev/sgb' [RET]

### 19.2.3 Scanning an Image

Netpbm
DEB: netpbm
RPM: netpbm
WWW: http://netpbm.sourceforge.net/

Use scanimage to scan an image. Most scanners let you specify the x and y values, in pixels, for the image size to scan, starting from the top-left corner of the scanner bed. Give these coordinates as arguments to the -x and -y options. Also, use the --resolution option to specify the scan resolution, with the argument given in dpi ("dots per inch"). Common resolution values include 72, 120, 204, 300, and 600 dpi; 72 dpi is the most popular resolution for use on the Web or for viewing on screen, and 204 dpi is often used for images that you want to send on a fax machine.

Scanned output is sent to standard output, so to scan an image to a file, redirect the standard output.
scanimage outputs images in the PNM ("portable anymap") formats, so make sure that you have the netpbm package (installed on most Linux systems by default); it's a useful collection of tools for converting and manipulating these common formats. The three PNM formats output by scanimage are as follows:

| PPM | Color images |
| PBM | Black and white images |
| PGM | Grayscale images |

Use the code-mode option to specify the format of the output, followed by one of the following arguments: "color" for color PPM, "gray" for PGM grayscale, or "lineart" for black and white PBM. Each scanner has a default mode; for most color scanners, the default mode will be "color."

⇒ Here are two ways to use this.

- - To make a 72 dpi scan of a color image 200 pixels wide and 100 pixels tall, using the UMAX scanner from previous examples, and writing to a file called scan.ppm, type (all on one line):
- ```
$ scanimage -d umax:/dev/sgb --resolution 72 -x 200 -y 100 > scan.ppm [RET]
```

- - To make a 300 dpi scan of a black and white image 180 pixels wide and 225 pixels tall, using the UMAX scanner from previous examples, and writing to a file called scan.pbm, type (all on one line):
- ```
$ scanimage -d umax:/dev/sgb --resolution 300 --mode lineart -x 180 -y 225 > scan.pbm [RET]
```

NOTES: The command lines in this recipe are split across two lines because they're too long to fit on one, but type these commands on one long line.

Once the image has been scanned and written to a file, you can edit it just as you would any image.

## 19.3 Extracting PhotoCD Images

Xpcd
DEB: xpcd
xpcd-gimp
RPM: xpcd
WWW: http://bytesex.org/xpcd.html

There are two methods to extract an image from a Kodak PhotoCD format
