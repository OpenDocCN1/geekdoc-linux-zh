+   - To display a .dvi file in an X window, type the following:

```
`$ xdvI filename.dvi`
```

+   - To print a .dvi file to a PCL printer, such as an HP LaserJet, type the following:

```
$ dvicopy filename.dvi
$ dvilj filename.dvi

```

+   - The **dviIj** command doesn't support virtual fonts directly. The **dvicopy** command converts the fonts so that the PCL printer can handle them.

# ### Converting documents

Documents can come to you in many different formats. Search just some of the Linux FTP sites on the Internet and you will find files in PostScript, DVI, man, PDF, HTML, and TeX. There is also a variety of graphics formats. Red Hat Linux comes with lots of utilities to convert documents and graphics from one format to another. The following is a list of document and graphics conversion utilities:

+   - **dos2unix** — Converts a DOS text file to a UNIX (Linux) text file.

+   - **fax2ps** — Converts TIFF facsimile image files to a compressed PostScript format. The PostScript output is optimized to send to a printer on a low-speed line. This format is less efficient for images with a lot of black or continuous tones. (In those cases, tiff2ps might be more effective.)

+   - **fax2tiff** — Converts fax data (Group 3 or Group 4) to a TIFF format. The output is either low-resolution or medium-resolution TIFF format.

+   - **g32pbm** — Converts a Group 3 fax file (either digifax or raw) to a portable bitmap.

+   - **gif2tiff** — Converts a GIF (87) file to a TIFF format.

+   - **man2html** — Converts a man page to an HTML format.

+   - **pal2rgb** — Converts a TIFF image (palette color) to a full-color RGB image.

+   - **pbm2g3** — Converts a portable bitmap image to a fax file (Group 3).

+   - **pdf2dsc** — Converts a PDF file to a PostScript document dsc file. The PostScript file conforms to Adobe Document Structuring Conventions (DSC). The output enables PostScript readers (such as Ghostview) to read the PDF file a page at a time.

+   - **pdf2ps** — Converts a PDF file to a PostScript file (level 2).

+   - **pfb2pfa** — Converts Type 1 PostScript font (binary MS-DOS) to ASCII-readable.

+   - **pk2bm** — Converts a TeX pkfont font file to a bitmap (ASCII file).

+   - **ppm2tiff** — Converts a PPM image file to a TIFF format.

+   - **ps2ascii** — Converts PostScript or PDF files to ASCII text.