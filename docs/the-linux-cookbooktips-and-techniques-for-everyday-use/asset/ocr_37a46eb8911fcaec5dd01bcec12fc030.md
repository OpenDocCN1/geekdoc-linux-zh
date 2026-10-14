`netpbm` package (installed on most Linux systems by default); it's a useful collection of tools for converting and manipulating these formats. The formats output by `scanimage` are as follows:

# FORMAT DESCRIPTION

+   PPM    Color images.
+   PBM    Black and white images.
+   PGM    Grayscale images.

Use the `--mode` option to specify the format of the output, followed by one of the following arguments: `color` for color PPM, `gray` for PGM grayscale, or `lineart` for black and white PBM. Each scanner has a default mode; for most color scanners, the default mode will be `color`.

+   To make a 72 dpi scan of a color image 200 pixels wide and 100 pixels tall, using the UNIX scanner from previous examples, and writing to a file called `scan.ppm`, type:

```
$ scanimage -d umax:/dev/sgb --resolution 72 -x 200 -y 100 62;
scan.ppm RET
```

+   To make a 300 dpi scan of a black and white image 180 pixels wide and 225 pixels tall, using the UMAX scanner from previous examples, and writing to a file called `scan.pbm`, type:

```
$ scanimage -d umax:/dev/sgb --resolution 300 --mode lineart
-x 180 -y 225 62; scan.pbm RET
```

> NOTE: The command lines in this recipe are split across two lines because they're too long to fit on one, but type these commands on one long line.

Once the image has been scanned and written to a file, you can edit it just as you would any image.

# 20.3 Extracting PhotoCD Images

@sf(Debian): `xpcd`
@sf(WWW): http://user.cs.tu-berlin.de/~kraxer/linux/xpcd/

There are two methods to extract an image from Kodak PhotoCD[30] ("PCD"). If you are browsing the disc with the xpcd tool, then choose an image, extract a copy at the desired resolution, and save it to a file, as described in Browsing PhotoCD Archives.

You can also use pcdtoppm on a PCD file directly to extract an image at a given resolution and save it to a file in PPM format. Use the `-r` option to specify the resolution to extract, given as a numeric argument from 1 (lowest resolution) to 5 (highest); if this option is omitted, a value of 3 is assumed. Also give as arguments the name of the PCD file to read from and the name of the PPM file to write to.