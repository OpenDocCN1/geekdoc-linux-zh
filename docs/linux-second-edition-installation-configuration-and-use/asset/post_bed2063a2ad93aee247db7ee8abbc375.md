
## 670 GIMP - THE PHOTOSHOP ALTERNATIVE

## GIF

This format is still the most popular Internet format for images and small animations. The bitmaps are compressed fairly efficiently and without losses, but the number of available colors is limited to 256. The format supports transparency (that is, a part of the rectangular bitmap is translucent). To save Gimp images as GIFs, you must first convert them to 256-color mode by means of IMAGE | INDEXED.

## JPEG

The format excels through an extraordinarily efficient compression algorithm, which is particularly suitable for photographs (not so much for technical drawings or screenshots). However, JPEG compression is not lossless, that is, JPEG images differ from the original. The differences are mostly invisible to the naked eye, if the quality factor for saving is set to a sufficiently high value. The default setting of 75 per cent is usually a sensible compromise.

> If a JPEG image is loaded, processed, and saved several times, the quality decreases with each cycle. While JPEG losses are practically invisible after the first time the algorithm has been used (provided the quality factor for saving was not set too low), changes add up in a rather disturbing way with multiple application. Therefore, the JPEG format is absolutely unsuitable for working copies! Save only the final image in JPEG format (and archive an XCF copy)!

## PNG

This format has been conceived as a successor for the GIF format and is better in every respect (no restriction to 256 colors, lossless in spite of better compression, and so on). As opposed to GIF, licensing problems no longer exist – the format (together with its source code) is freely available. However, PNG being a fairly recent format, older graphics programs and Web browsers are often incapable of handling PNG images.

## TIFF

This format is surprisingly popular in professional image processing, although the reasons are more historical. Images are saved without loss; (a relatively weak) compression is optional. There are numerous variations of the TIFF format, which sometimes makes the exchange of TIFF images between different programs quite problematic.

> If you work with layers, saving in bitmap formats only saves the current active layer, not the complete image composition! Therefore, always use the XCF format for your working copies. To save the final bitmap, you must combine the layers into a complete image by means of LAYERS | FLATTEN IMAGE. This hint also applies to saving images in PostScript format.

## BASICS 671

The PostScript format (PS, EPS) has a good reputation as the format for professional exchange of images. However, this reputation only refers to text and vector graphics, not to bitmaps!

You should save images in PostScript format only if you want to use the file at a later time in a different program (for example, a text processing or typesetting program). Here, two options are of interest:

ENCAPSULATED POSTSCRIPT means that a comment is stored at the beginning of the PostScript file, which specifies the coordinate range of the image. This information is required for correct incorporation of the image in another program. PostScript files intended for further use in other programs (and not for printing) usually bear the extension .eps (not simply .ps)

PREVIEW means, in addition to the PostScript commands, a bitmap is stored which allows a preview even in programs that have no access to a PostScript interpreter. This preview bitmap, however, increases the file size considerably without adding any information relevant for printing. You should therefore activate this option only if you want to use the PostScript file on Windows or Apple computers where usually no gs is installed for an easy PostScript preview.

Gimp can also read PostScript and PDF files. PDF is a format for document distribution by Adobe, which essentially consists of tightly compressed PostScript code. PDF documents are usually read with the aid of acread.

For the import, Gimp uses the gs PostScript interpreter. The attainable quality is improved by two options: a HIGH RESOL yields large bitmaps (which can be optimized and reduced in Gimp), the ANTIALIAS options cause gs itself to generate a high-resolution bitmap and subsequently reduce it. This allows the color of the individual pixels to be derived from several points, giving rise to greyscales and halftones which make the image appear more sharply defined.

## XCF and PSD

XCF is Gimp's proprietary data format. It is the only format in which definitely all processing information (masks, layers, current selection, and so on) is stored. The file is not compressed. While an image is being elaborated, XCF is the only suitable format for working copies.

The PSD format is the Photoshop counterpart to XCF. Gimp can only read PSD files, but not write them (and it is rather improbable that Photoshop will get a Gimp import filter in the future).

The following rules apply to all formats: if saving you append the extensions *.gz or *.bz2 to the file name, the file is automatically compressed. Obviously, this is only sensible if the file format does not already include compression itself (such as JPEG, GIF, and PNG). Obviously, files with these extensions are automatically decompressed again during loading. bzip2 compresses slightly better than gzip, but is significantly slower. The following results were achieved with a test file: .xzf 250 Kobytes, .xzf 100 Kobytes.

![](img/b30873dd3d753687a59253fb9ad26a0b_698_0.png)

## 20.4 Paint tools

With paint tools as PENCIL, PAINTBRUSH, and AIRBRUSH, you can create entirely new graphics or modify existing images. You should, however, always bear in mind that Gimp is a pixel-oriented image processing program, not a vector-oriented one: the result of a paint operation is a number of modified pixels. Gimp does not store any information about the drawn object; therefore, it can no longer be manipulated at a later stage.

First experiments with paint tools are best carried out in an empty image. This allows you to easily cancel unwanted results by means of D (default colors), Ctrl+A (select all), and Ctrl+X (cut). To experiment with colors, you can quickly create a colorful image with filters | RENDER | PLASMA.

Gimp lacks even the most trivial draw commands – for example to draw a rectangle or a circle. This does, however, not mean that this is impossible in Gimp! One alternative is to use selections – more about this page 680 onwards. Another alternative is provided by the filters | RENDER | GIF tool which is, however, not described in this chapter.

The proper alternative, that is, to employ true vector-oriented drawing programs, is difficult under Linux. The choice is still limited. Probably the most powerful program is tgraf – but its user interface makes you realize that the program is relatively old.

## Pencil, Paintbrush, Airbrush, Erase

The paint tools PENCIL (Shift+P), PAINTBRUSH (P), and AIRBRUSH (A) are closely related to each other. All three tools use the shape in the BRUSH dialog as a painting device. While the PENCIL interprets this as a black and white pattern and therefore yields very sharp edges, the PAINTBR also considers grayscales.

![](img/b30873dd3d753687a59253fb9ad26a0b_699_0.png)

Figure 20.6 Examples of the application of Pencil (top), Paintbrush, and Airbrush (bottom).

## PAINT TOOLS 673

With the AIRBRUSH, processing time comes into play: the longer the spraycan is applied or the more often it is moved over a point, the more intense the result. Intensity per time and mouse movement can be controlled via options. 20.6 shows all three tools, employing the same pattern.

At first sight, ERASE (Shift+E) seems to represent just the inverse of PAINTBRUSH, employing the background color instead of the foreground color. However, the difference becomes visible when the tool is employed in so-called float-ing selections (see next section): here, the selected area is reduced by the tool shape.

If you want to paint or delete a straight line with any of the four tools, quickly press the mouse button at the starting point. Then, move the mouse to the target point and briefly press the mouse button again, this time in combination with the Shift key.

## Filling with colors and patterns (BUCKET FILL)

With BUCKET FILL (Shift+B), you can fill a color-delimited area with the fore-ground or with a pattern set in the DIALOGS | PATTERNS dialog. If you click the mouse button in combination with Shift+C the tool fills the area with the back-ground color (only with FILL).

![](img/b30873dd3d753687a59253fb9ad26a0b_700_0.png)

Figure 20.7 Patterns and options for BUCK FILL.

In the default setting, the tool covers the contiguous area of all pixels whose colors differ by a maximum of 15 units from the starting point (a unit scale from 0 to 255). The value range can be changed with FILL THRESHOLD in the options dialog. In Figure 20.8, FILL was applied with a tile-shaped pattern and a reduced OPACITY (50) to the medium grayshades.

> Limitation to a color area applies only if no selection is present! If a selection-exists, it is filled completely, that is, without regard for the colors of its contents. To prevent this, you can either unmark the selection with Shift+Ctrl+A, or convert it into a floating selection with SELECT | FLOAT.
