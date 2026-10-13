
## TABLE 16.1 CONTINUED

| Format | Type | Conversion Program |
|---|---|---|
|  |  | giftoppm |
|  |  | gif2tiff |
|  |  | gimp |
|  |  | ppmtogif |
|  |  | convert |
|  |  | xv |
| .gif87 | Graphic Interchange | convert |
|  |  | xv |
| .go | Compressed GraphOn | pbmtogo |
| .gould | Gould scanner file | gouldtoppm |
| .icn | Sun icon | icontopbm |
|  |  | pbmtoicon |
| .ico | Microsoft icon | convert |
| .ilbm | IFF ILBM file | ilbmtoppm |
|  |  | ppmtolbm |
| .img | GEM image file | gemtopbm |
|  |  | pbmtogem |
|  |  | imgtoppm |
| .icr | NCSA ICR raster | ppmtolicr |
| .jbig | Joint Bi-level Image Group | convert |
| .jpeg | Joint Photographic Experts Group | cjpeg |
|  |  | djpeg |
|  |  | jpegtran |
|  |  | convert |
|  |  | gimp |
|  |  | xv |
| .lj | HP LaserJet data | pbmtolj |
| .ln03 | DEC LN03+ Sixel output | pbmtoln03 |
| .mgr | MGR bitmap | mgrtopbm |
|  |  | pbmtomgr |
| .miff | MNG multiple-image network | convert |
| .mitsu | Mitsubishi S340-10 file | ppmtomitsu |
| .mpeg | Motion Picture Group | convert |
| .mtv | MTV ray tracer | mtvtopp m, convert |
| .pbm | Portable bitmap | pbm*, convert, xv |
| .pcd | Photo CD | convert |
| .pcl | HP PaintJet PCL | ppmtopixl, convert |
| .pcx | PCX graphics | pcxtoppm, ppmtopcx, convert, gimp, xv |
| .pdf | Portable Document Format | convert, xpdf |
| .pgm | Portable graymap | pbmtopgm, pgmtoppm, ppmtopgm, convert, cjpeg, xv |
| .pi1 | Atari Degas file | pi1toppm, ppmtopi1 |
| .pi3 | Atari Degas file | pbmtopi3, pi3topbm |
| .pict | Macintosh PICT file | pictoppm, ppmtopict, convert |
| .pj | HP PaintJet file | pjtoppm, ppmtopj |
| .pk | PK format font | pbmtopk, pktopbm |
| .plasma | Plasma fractal | convert |
| .plot | UNIX plot file | pbmtoplplot |
| .png | Portable Network Graphic | pngtopnm, pnmto png, convert, gimp, xv |
| .pnm | Portable anymap | pnm*, convert, gimp |
| .pnt | MacPaint file | macptopbm, pbmtomacp |
| .ppm | Portable pixmap | ppm*, cjpeg, convert, xv |
| .ps | PostScript (lines) | pbmtops, pnmtops, convert, xv, gimp, gv |
| .psd | Adobe Photoshop bitmap | convert |
| .ptx | Printronix printer graphics | pbmtoptx |
| .qrt | QRT ray tracer | qrttoppm |
| .rad | Radiance image | convert |
| .ras | Sun rasterfile | pnmtorast, rasttopnm, gimp |
| .rla | Alias/Wavefront image | xv |
|  |  | convert (read-only) |
| .rle | Utah run-length encoded | convert (read-only) |
|  |  | xv |
| .sgi | Silicon Graphics image | pnmtosgi |
|  |  | sgitopnm |
|  |  | convert |
| .sir | Solitaire graphics | pnmtosir |
|  |  | sirtopnm |
| .sixel | DEC sixel format | ppmtosixel |
| .spc | Atari Spectrum file | spctoppm |
| .spu | Atari Spectrum file | sputoppm |
| .sun | Sun rasterfile | convert |
|  |  | gimp |
| .tga | TrueVision Targa file | ppmtotga |
|  |  | tgatoppm |
|  |  | convert |
|  |  | gimp |
|  |  | xv |
| .tiff | Tagged File Format | pnmtotiff |
|  |  | tiff topnm |
|  |  | ppmtotiff |
|  |  | tiff2ps |
|  |  | convert |
|  |  | gimp |
|  |  | xv |
| .tiff24 | Tagged file Format (24-bit) | convert |
|  |  | xv |
| .tim | PSX TIM | convert |
| .ttf | TrueType font file | convert |
| .txt | text file bitmap | pbmtext |
|  |  | convert (read-only) |
| .uil | Motif UIL icon | ppmtoiuil |
|  |  | convert |
| .upc | Universal Product Code | pbmupc |
| .uyvy | 16-bit YUV format | convert |
| .vicar |  | convert (read-only) |
|  |  | xv |
| .viff | Khoros Visualization image | convert |
| .x10bm | X10 bitmap | pbmtox10bm |
| .xbm | X11 bitmap | pbmtoxbm |
|  |  | xbm topbm |
|  |  | convert |
|  |  | xv |
| .xim | Xim file | ximtoppm |
| .xpm | X11 pixmap | ppmtoxpm |
|  |  | xpmtoppm |
|  |  | convert |
|  |  | gimp |
|  |  | xv |
| .xv | xv thumbnail | xvminitoppm |
| .xvpic | xv thumbnail file | xvpictoppm |
| .xwd | X11 Window Dump | ppmtoxwd |
|  |  | xwdtopnm |
|  |  | convert |
|  |  | gimp |
|  |  | xv |
| .ybm | Bennet Yee face file | pbmtoybm |
|  |  | ybmtopbm |
| .yuv | Abekas YUV file | ppmtoyuv |
|  |  | yuvtoppm |
|  |  | convert |
| .zeiss | Zeiss confocal file | zeisstoppm |
| .zinc | Zinc bitmap | pbmtozinc |

## Converting and Viewing Graphics

There are a number of ways to convert graphic files to different formats using the programs installed on your system. Several of the painting or drawing programs discussed in this hour translate graphics, and many programs in Table 16.1 also work as filters in piped commands (see Hour 6, "Using the Shell," for details) to translate graphics.

You can use different combinations of these commands to convert files. OpenLinux users, such as graphics artists or system administrators, convert files for different reasons. Artists or casual users might want to import or export graphics for use by different drawing programs. System administrators might look for a side benefit of converting graphics to save disk space. In some instances, the savings can be considerable. Look at the following example:

```
# xwd >graphic.xwd
# xwdtopnm <graphic.xwd | convert - graphic.jpg
xwdtopnm: writing PPM file
# ls -l graphic.*
-rw-r--r-- 1 bball users 11003 Jan 27 14:21 graphic.jpg
-rw-r--r-- 1 bball users 851523 Jan 27 14:17 graphic.xwd
```

The first command line uses the xwd client to create an X11 window dump graphics file (.xwd) after you select a window and press your left mouse button. The window dump file is converted to .pnm format with the xwdtopnm command, and the output stream is fed into the convert command to create a .jpg graphics file. The hyphen (-) following the convert command specifies that the standard input should be used in lieu of an input filename. As you can see, the .jpg graphics file is more than 77 times smaller than the X11 window dump graphics file!

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_388_0.png)

> Results and benefits of file compression vary, depending on the size of the graphics file and compression settings. See the convert man page for details.

There are also many graphics programs not listed in Table 16.1 that can be used to alter graphics images. For example, the pnrotate, pnmsmooth, and pnmscale commands rotate, smooth, and resize graphics images. You can use a variety of these programs to not only convert graphics, but change their appearance or orientation.

If you’re using pipes to convert graphics, you also can change the images on-the-fly by applying these filter programs. For example, if you have a graphics file in .xpm format
but want to quickly flip it upside down and save it in .gif format, apply a filter program such as the pnmtflip command:

```
# xpmtoppm penguin.xpm | pnmtflip -topbottom | convert - penguin.gif
```

Here the file penguin.xpm is converted from .xpm format to .ppm format. The output of the xpmtoppm command is fed to the pnmtflip command, which flips the graphics file upside down with the -topbottom option. The output of the pnmtflip command is fed to the convert command, which reads the standard input and saves the graphics stream in .gif format.

Combinations of different filters achieve different effects. For other effects, see such commands as pnmcrop, pnminvert, pnmrotate, pnmscale, pnmsmooth, or pnmtile.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_389_0.png)

> Not all graphics conversion programs included with your Linux distribution read the standard input and write to the standard output. Read the manual pages for any desired conversion programs before experimenting with pipes on the command line.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_389_1.png)

> Preview or print the results of your conversions before discarding original files to make sure you achieve the effect you want and that the resulting graphics file does not suffer loss of image quality.

If you experiment with complex pipes, use the convert command, one of seven programs in the ImageMagick package (discussed later in the section “Graphics Editing with ImageMagick”) for easier file conversions. This command, found under the /usr/bin directory, translates more than 75 different graphics file formats (even some not listed in Table 16.1).

The convert program normally works by recognizing different file extensions on the command line, as shown in the following example:

```
# xwd >graphic.xwd
# convert graphic.xwd graphic.tiff
```

Here, the xwd client is used to create an X11 window dump graphics file. The convert command then creates a .tiff file by specifying the .tiff extension on the second, or output, file on the command line. For details about using the convert command, see the ImageMagick and convert command man pages.
