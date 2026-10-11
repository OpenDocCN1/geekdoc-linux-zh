**NOTE**

There is an important difference between two similar MIME types in CUPS: one is `application/postscript`, the other is `application/vnd.cups-postscript`. While `application/postscript` is meant to be device-independent, job options for the file are still outside the PS file content, embedded in command-line or environment variables by CUPS, `application/vnd.cups-postscript` may have the job options inserted into the PostScript data itself (where applicable). The transformation of the generic PostScript (`application/postscript`) to the device-specific version (`application/vnd.cups-postscript`) is the responsibility of the CUPS `pstops` filter. pstops uses information contained in the PPD to do the transformation.

CUPS can handle ASCII text. HP-GL, PDF, PostScript, DVI. and many image formats (GIF, PNG, TIFF, JPEG, Photo-CD, SUN-Raster, PNM, PBM, SGI-RGB, and more) and their associated MIME types with its filters.

# **21.5.2 MIME Type Conversion Rules**

CUPS reads the file `/etc/cups/mime.conv` (and all other files named with a `*.conv` suffix in the same directory) upon startupt. These files contain lines naming an input MIME type, an output MIME type, a format conversion filter that can produce the output from the input type, and virtual costs associated with this conversion. One example line reads like this:

```
```
application/pdf    application/postscript    33    pdftops
```
```

This means that the `pdftops` filter will take `application/pdf` as input and produce `application/postscript` as output; the virtual cost of this operation is 33 CUPS-$. The next filter is more expensive, costing 66 CUPS-$:

```
```
application/vnd.hp-HPGl application/postscript    66    hpgltops
```
```

This is the `hpgltops`, which processes HP-GL plotter files to PostScript.

```
```
application/octet-stream
```
```

Here are two more examples: