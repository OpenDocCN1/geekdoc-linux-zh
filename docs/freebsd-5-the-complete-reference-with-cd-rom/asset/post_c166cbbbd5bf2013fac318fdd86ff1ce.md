
is interpreted as horizontal and vertical resolutions. A single value is interpreted as both horizontal and vertical resolutions, so `-r72` is equivalent to `-r72x72`.

- `-sDEVICE=jpeg` This option sets the output format—JPEG in this case. Other options are described shortly.
- `-sOUTPUTFILE=file.jpg` This option specifies the output filename. If you omit it, Ghostscript assumes standard output, which is likely to produce either a lot of beeping and a corrupted display or a window in which the output appears as a graphic for x11 and related output formats.
- `file.ps` The final option is the input filename. When using Ghostscript in a script, it's common to see a single dash (-) as the input filename, signifying standard input.

You can give Ghostscript input files in the form of PostScript, EPS, or PDF. To obtain a complete list of output file formats, type `gs --help`. The resulting output includes a long list of output devices. These aren't always entirely obvious, but most of the ones relating to other standard graphics file formats (as opposed to printer formats) are fairly obvious. Some of the more noteworthy graphics file options include:

- **BMP files** The .bmp filename extension is associated with an old but still fairly common bitmap file format. Ghostscript provides several bitmap output options, including `bmpmono`, `bmpgray`, `bmp16`, `bmp256`, and `bmp16m`. These options differ in their color depth and type.
- **PCX files** The old PC Paintbrush program used files with an extension of .pcx, and Ghostscript can produce such files, using output driver codes of `pcxmono`, `pcxgray`, `pcx16`, `pcx256`, `pcx24b`, or `pcxemxvk`. As with BMP output, the PCX output options create files of varying color depth and encoding methods.
- **TIFF files** Ghostscript can create the common TIFF format with its `tiff12nc`, `tiff42nc`, `tiff12zw`, and `tiffpack` options. The last two of these options enable TIFF's compression features.
- **PNG files** Ghostscript's `pngmono`, `pnggray`, `png16`, `png256`, and `png16m` output options create PNG files of varying color types and depths.
- **JPEG files** There are only two JPEG options: `jpeg` and `jpeggray`, which create color and gray-scale JPEG files, respectively.
- **Postscript files** You can create PostScript output with the `psmono`, `psgray`, `psrgb`, and `pswrite` options.
- **EPS files** The `epswrite` option creates an EPS file.
- **PDF files** The `pdfwrite` option creates a PDF file.

Creating PostScript or a related format from the same file type may sound odd, but it can be quite useful. The output PostScript file is actually a PostScript bitmap, so if you send it to a printer, the printer will process it differently than it would process the original. This fact can be useful if the original file is complex or contains subtle errors that cause problems for a printer; Ghostscript may be able to “predigest” the file, making it easier for a printer with limited memory or a buggy PostScript interpreter to handle.

Most of the output Ghostscript file types are bitmaps, but PDF files are an exception; PDF files contain fonts and are essentially vector graphics files. PDF is a popular format for distributing text electronically, and Ghostscript can be a useful tool for creating such files. You can create a document in a word processor, LaTeX, or in some other way, then “print” it to a PostScript file and run the result through Ghostscript to create a PDF file. The resulting file can be read in PDF viewers on any platform.

## Using GUI PostScript Viewers

Sometimes it’s desirable to view a PostScript file before printing it. For instance, you might want to be sure you’re printing the correct file before devoting a hundred pages to the document. Ghostscript enables you to perform this preview operation, either by itself or through a more GUI-oriented front-end. In the simplest case, you can issue a truncated `gs` command similar to the one presented earlier, in “Using Ghostscript”:

```bash
$ gs -dBATCH -dSAFER -dDEVICE=x11 file.ps
```

The result of issuing this command is an X window that displays the document. Ghostscript displays the following prompt in the xterm window in which you typed the command:

> >>showpage, press <return> to continue<<

Pressing ENTER displays the next page of the document, until you reach the end, at which point Ghostscript exits. This simple method may be acceptable for short documents or if you don’t need to page back and forth through a document, but it’s not enough for some purposes. If you need to be able to move to arbitrary pages, zoom in and out, or perform other actions, you may want to use a GUI front-end to Ghostscript. Such tools enable these more advanced options. Examples of these programs include:

- **Ghostview** This program is the basic Ghostscript front-end. It can be called by typing `ghostview`, optionally followed by the name of the file you want to view. This program’s user interface is quite primitive by modern standards.
- **gv** This program is derived from Ghostview, but adds more options and a more modern user interface. It’s used much like Ghostview, but its program name is *gv*.
- **GNOME Ghostview** As you might guess from the name, this program is part of the GNOME project. It’s very similar to *gv* in operation, aside from differences in widget sets and a few features. The program’s filename is *ggv*.

These programs all ship with FreeBSD and are available in packages or ports named after the programs in question (*ghostview*, *gv*, or *ggv*) in the *printing* area. Using any of these programs is fairly straightforward: type the program name, optionally followed by the name of the file you want to view. All of these programs use Ghostscript to do the rendering, so they produce very similar results. GNOME Ghostview and *gv* offer some extra options, though, such as *anti-aliasing* of fonts (aka *font smoothing*), a technique that can improve font legibility in some cases. These programs can all display PostScript, EPS, and PDF files, although some PDF features don’t render correctly.

Figure 26-7 shows GNOME Ghostview in operation, displaying a PostScript file. The bulk of the window is dominated by the file being displayed, but there are various GUI controls, as well. Most important, the left side of the window hosts a page list. You can move about in the document by double-clicking a page number. This doesn’t work properly in all documents, though; with some, you can only move forward or backward one page at a time. You can also zoom in or out using the magnifying glass icons, change the orientation of the virtual page using options under the *Document | Orientation* menu, and adjust options such as whether or not to use anti-aliasing from the *Settings | Preferences* dialog box. These programs also enable you to print the entire document or just a range of pages, which can be a convenient option if you want to print just a few pages from a large document.

### Using GUI PDF Viewers

As noted in the previous section, common GUI PostScript viewers support PDF files as well as PostScript and EPS files. There are, however, a few additional options that work only on PDF files. The two most important of these are:

- **Xpdf** This program is an open source X-based PDF viewer. Its features are fairly simple; its main window is dominated by a view of the document, it has no menu bar, and it uses a few buttons along its bottom border to page through the document, search for text, or print the file.
- **Acrobat Reader** Adobe’s PDF viewer is arguably the standard against which all others must be judged because Adobe originated the PDF format (and PostScript, for that matter). You can install the Acrobat Reader from the *acroread4* package or port—but this program is technically not a FreeBSD program; it’s a Linux program that relies upon FreeBSD’s Linux binary compatibility, as described in Chapter 4.
