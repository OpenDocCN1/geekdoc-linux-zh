
This command combines the two images and writes a new image file, `picture.jpeg`, whose contents contain 70 percent of the first image.

> NOTE: Use `-blend 50` to blend the two source files equally.

## 19.1.8 Morphing Two Images Together

Morphing is a method of computer imaging for finding the difference between the shapes in two images; it's often used in special effects to transform aspects of two creatures, such as the faces of a human and some other animal.

You can use combine to get a morph-like effect by giving the difference argument to the `-compose` option. When specified with two input images and an output file, this command takes the difference between corresponding pixels in the two images; the effect is like a "morphed" image.

- To make a morphed image of the files `ashes.jpeg` and `phoenix.jpeg`, and write it to `picture.jpeg`, type:

```
$ combine -compose difference ashes.jpeg phoenix.jpeg picture.jpeg RET
```

The result in file `picture.jpeg` is:

![](img/8bf3d083d04b4cc3d79bd39657ac711a_292_0.png)

> NOTE: `x morph` is a tool for morphing images; see Interactive Image Editors and Tools.

## 19.2 Converting Images between Formats

@sf(Debian): `imagemagick`
@sf(WWW): `ftp://ftp.wizards.dupont.com/pub/ImageMagick/`

Use convert to convert the file format of an image. Give the name of the file to convert as the first argument, and the destination file as the second argument. When you convert a file, the original is not altered.

To specify the file type to convert to, use that file type's standard file extension in the file name of the converted file.

- To convert the JPEG file `phoenix.jpeg` to a PNG image, type:

```
$ convert phoenix.jpeg phoenix.png RET
```

This command converts the JPEG image `phoenix.jpeg` to PNG format and writes it to a new file, `phoenix.png`.

The following table lists the file extensions to use and describes their format. (The convention is to give extensions in all lowercase letters.)

| FILE EXTENSION | IMAGE FORMAT |
|---|---|
| bmp | Microsoft Windows bitmap image. |
| cgm | Computer Graphics Metafile format. |
| cmyk | Raw cyan, magenta, yellow, and black bytes. |
| eps | Adobe Encapsulated PostScript. |
| fax | Group 3 fax format. |
| fig | TransFig image format. |
| fpx | FlashPix format. |
| gif | CompuServe Graphics Interchange Format, version GIF89a (usually pronounced "giff," rhyming with "biff"). |
| gray | Raw gray bytes. |
| jpeg and jpg | Joint Photographic Experts Group JFIF format (usually pronounced "jay-peg"). |
| pbm | Black and white portable bitmap format. |
| pcd | Kodak PhotoCD format, 512x768 pixels maximum resolution. |
| pcl | Page Control Language format. |
| pcx | ZSoft IBM PC Paintbrush format. |
| pdf | Adobe Portable Document Format. |
| pict | Apple Macintosh QuickDraw format. |
| png | Portable Network Graphics format (usually pronounced "ping"). |
| pnm | Portable "anymap" format. |
| ppm | Color portable pixmap format. |
| ps | Adobe PostScript format. |
| rgb | Raw red, green, and blue bytes. |
| tga | TrueVision Targa image format. |
| tiff and tif | Tagged Image File Format (usually pronounced "tiff"). |
| xbm | X Window System bitmap format. |
| xpm | Color X Window System pixmap format. |
| xwd | Color X Window System window "dump" file format. |

## The Linux Cookbook: Tips and Techniques for Everyday Use:

When converting a file to JPEG format, be sure to use the `-interlace NONE` option to make sure the resultant JPEG image is non-interlaced—unless, of course, you want an interlaced image; an interlaced image is drawn in multiple passes, and is often used on the Web where a reader may view the low-resolution image consisting of early passes before the entire image is downloaded. A non-interlaced image is drawn in one single pass.

For example, use convert to convert a PNM file to non-interlaced JPEG, while sharpening it, adding a border, and adding a copyright statement.

- To convert the PNM file `pike.pnm` to non-interlaced JPEG while sharpening the image by 50 percent and adding both a 2x2 border and a copyright comment, type:

```
$ convert -interlace NONE -sharpen 50 -border 2x2
-comment 'copyright 1999 MS' pike.pnm pike.jpeg RET
```

This command writes its output to a file `pike.jpeg`. Notice that the options `-border` and `-comment` were previously described for the `mogrify` tool. Some ImageMagick tools share common options, which is useful if you are making multiple changes to an image file at once; only one tool is needed for the job.

NOTE: Some image formats are "lossy," in that some image information is lost when you convert to it. For example, the JPEG format is a lossy format that is usually used for photographic images. If you convert a file from its source PNM format to JPEG and then back to PNM, the resultant PNM will not be identical to the original source PNM.

To convert image files interactively, use the GIMP to open the image, and then choose `Save as` from the File menu, and select the file type to use; see Editing Images with the GIMP.
