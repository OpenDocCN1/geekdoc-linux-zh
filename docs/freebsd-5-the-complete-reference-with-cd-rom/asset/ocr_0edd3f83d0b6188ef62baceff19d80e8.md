is interpreted as horizontal and vertical resolutions. A single value is interpreted as both horizontal and vertical resolutions, so `-r72` is equivalent to `-r72x72`.

+   *   `-sDEVICE=jpeg` This option sets the output format—JPEG in this case. Other options are described shortly.

+   *   `-sOUTPUTFILE=file.jpg` This option specifies the output filename. If you omit it, Ghostscript assumes standard output, which is likely to produce either a lot of beeping and a corrupted display or a window in which the output appears as a graphic for x11 and related output formats.

+   *   `file.ps` The final option is the input filename. When using Ghostscript in a script, it's common to see a single dash (-) as the input filename, signifying standard input.

You can give Ghostscript input files in the form of PostScript, EPS, or PDF. To obtain a complete list of output file formats, type `gs --help`. The resulting output includes a long list of output devices. These aren't always entirely obvious, but most of the ones relating to other standard graphics file formats (as opposed to printer formats) are fairly obvious. Some of the more noteworthy graphics file options include

+   *   **BMP files** The .bmp filename extension is associated with an old but still fairly common bitmap file format. Ghostscript provides several bitmap output options, including `bmpmono`, `bmpgray`, `bmp16`, `bmp256`, and `bmp16m`. These options differ in their color depth and type.

+   *   **PCX files** The old PC Paintbrush program used files with an extension of .pcx, and Ghostscript can produce such files, using output driver codes of `pcxmono`, `pcxgray`, `pcx16`, `pcx256`, `pcx24b`, or `pcxemxvk`. As with BMP output, the PCX output options create files of varying color depth and encoding methods.

+   *   **TIFF files** Ghostscript can create the common TIFF format with its `tiff12nc`, `tiff42nc`, `tiff12zw`, and `tiffpack` options. The last two of these options enable TIFF's compression features.

+   *   **PNG files** Ghostscript's `pngmono`, `pnggray`, `png16`, `png256`, and `png16m` output options create PNG files of varying color types and depths.

+   *   **JPEG files** There are only two JPEG options: `jpeg` and `jpeggray`, which create color and gray-scale JPEG files, respectively.

+   *   **Postscript files** You can create PostScript output with the `psmono`, `psgray`, `psrgb`, and `pswrite` options.

+   *   **EPS files** The `epswrite` option creates an EPS file.

+   *   **PDF files** The `pdfwrite` option creates a PDF file.