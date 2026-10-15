# #94 A Smarter Image Size Analyzer

The file command offers the ability to ascertain the file type and, in some cases, the dimensions of an image. But too often it fails:

```
$ file * | head -4
100_0399.png:    PNG image data, 1024 x 768, 8-bit/color RGBA, non-interlaced
8t grade art1.jpeg: JPEG image data, JFIF standard 1.01
99icon.gif:      GIF image data, version 89a, 143 x 163
Angel.jpg:       JPEG image data, JFIF standard 1.01
```

PNG and GIF files work, but what about the more common JPEG? The file command can't figure out the image's dimensions. Annoying!

# The Code

Let's fix that with a script (Listing 14-1) that uses the identify tool from ImageMagick to far more accurately ascertain image dimensions.

```
#!/bin/bash
# imagesize- Displays image file information and dimensions using the
# identify utility from ImageMagick

for name in *
do
  identify -format "%f: %G with %k colors.\n" "$name"
done
exit 0
```

Listing 14-1: The imagesize script

# How It Works

When you use the -verbose flag, the identify tool extracts an extraordinary amount of information about each image analyzed, as shown in its output for just one PNG graphic:

```
$ identify -verbose testimage.png
Image: testimage.png
Format: PNG (Portable Network Graphics)
Class: DirectClass
Geometry: 1172x158+0+0
Resolution: 72x72
Print size: 16.2778x2.19444
Units: Undefined

--snip--

Profiles:
Profile-icc: 3144 bytes
IEC 61966-2.1 Default RGB colour space - sRGB
```