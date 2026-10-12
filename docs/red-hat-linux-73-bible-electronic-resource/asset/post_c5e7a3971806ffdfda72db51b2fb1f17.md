
Each command defines some action to be taken. The action can control page layout, the font used, spacing, paragraph layout, or a variety of other actions on the document. The minimum amount of formatting that a LaTeX document can contain is the following:

```latex
\documentclass{name}
\begin{document}
    TEXT GOES HERE!
\end{document}
```

You should replace `{name}` with the name of the class of document you are creating. Valid document classes include article, book, letter, report, and slides. The text for the file, along with your formatting commands, goes between the *begin* and *end* document commands.

The best way to get started with LaTeX is to use the LyX editor. LyX provides a GUI for creating LaTeX documents. It also contains a variety of templates you can use instead of just creating a document from scratch. Figure 6-8 shows an example of the LyX editor.

![](img/1744bde8c889adfab3fc911e1687fecf_251_0.png)

Figure 6-8: Create LaTeX documents graphically with the LyX editor.

> **NOTE:** The LyX editor doesn't come with the Red Hat Linux distribution. Find an RPM package for LyX from the LyX FTP site at `ftp://ftp.lyx.org/pub/lyx/bin`. Besides needing to have several tetex packages installed, to install LyX you will also need the xforms package.

If you want to edit LaTeX in a regular text editor, you need to be familiar with the LaTeX commands. For a complete listing of the LaTeX commands, type `$ info latex` and then go to the section “Commands within a LaTeX document.”

## Using the LyX LaTeX Editor

Start the LyX LaTeX editor with the `lyx` command. LyX comes with a lot of supporting documentation. Click Help to select a Tutorial, User's Guide, or other information.

To start your first document, I recommend that you select one of the templates provided with LyX. Templates are located in `/usr/share/lyx/templates`. To open a template, click File → New from template, and select Templates. There are templates available for a letter, technical paper, and a Linux document, to name a few.

Besides offering standard editing functions, such as cut, copy, and paste, you can perform a variety of markup functions from the Layout menu. As for mathematical functions, the Math menu enables you to insert fractions, square root, exponent, sum, and integral functions into your document. When you are done, you can:

- Print the file to a PostScript printer or output a PostScript (.ps) file. (Click File → Print, select the printing method, and then click OK.)
- Output the file to dvi format. (Click File → View.dvi.) Your document will appear in the xdvf window, which displays how the document will appear when it is printed.
- Export the file to LaTeX, DVI, PostScript, or ASCII Text. (Click File → Export and choose from the list of file formats.)

LyX calls itself a WYSIWYM editor — What You Say Is What You Mean. As a result, what you see on the screen as you edit is not exactly what the printed document will look like. For example, no extra white space will appear between lines by pressing Enter multiple times.

Because LyX supports style files, it enables you to create documents that meet several different standards. For example, LyX supports typesetting for the American Mathematics Society (AMS) journals using the article textclass. Other textclasses supported include:

- **article** — One-sided paper with no chapters.
- **report** — Two-sided report, tending to be longer than an article.
- **book** — Same as report, with additional front and back matter.
- **slides** — For producing transparencies.
- **letter** — Includes special environments for addresses, signatures, and other elements.

## Printing LaTeX files

Whether you create your own LaTeX file, export one from the LyX LaTeX editor, or download one from the Internet, several utilities are available to format, print, or display the output. Here are some of your choices:

- To format a LaTeX file (filename.tex), run the following command:

```bash
$ latex filename.tex
```

- To print a .dvi file (filename.dvi), send it to your default PostScript printer, and type the following:

```bash
$ dvips filename.dvi
```

- To display a .dvi file in an X window, type the following:

```bash
$ xdvf filename.dvi
```

- To print a .dvi file to a PCL printer, such as an HP LaserJet, type the following:

```bash
$ dvicopy filename.dvi
$ dvilj filename.dvi
```

- The **dvilj** command doesn't support virtual fonts directly. The **dvicopy** command converts the fonts so that the PCL printer can handle them.

### Converting documents

Documents can come to you in many different formats. Search just some of the Linux FTP sites on the Internet and you will find files in PostScript, DVI, man, PDF, HTML, and TeX. There is also a variety of graphics formats. Red Hat Linux comes with lots of utilities to convert documents and graphics from one format to another. The following is a list of document and graphics conversion utilities:

- **dos2unix** — Converts a DOS text file to a UNIX (Linux) text file.
- **fax2ps** — Converts TIFF facsimile image files to a compressed PostScript format. The PostScript output is optimized to send to a printer on a low-speed line. This format is less efficient for images with a lot of black or continuous tones. (In those cases, tiff2ps might be more effective.)
- **fax2tiff** — Converts fax data (Group 3 or Group 4) to a TIFF format. The output is either low-resolution or medium-resolution TIFF format.
- **g32pbm** — Converts a Group 3 fax file (either digifax or raw) to a portable bitmap.
- **gif2tiff** — Converts a GIF (87) file to a TIFF format.
- **man2html** — Converts a man page to an HTML format.
- **pal2rgb** — Converts a TIFF image (palette color) to a full-color RGB image.
- **pbm2g3** — Converts a portable bitmap image to a fax file (Group 3).
- **pdf2dsc** — Converts a PDF file to a PostScript document dsc file. The PostScript file conforms to Adobe Document Structuring Conventions (DSC). The output enables PostScript readers (such as Ghostview) to read the PDF file a page at a time.
- **pdf2ps** — Converts a PDF file to a PostScript file (level 2).
- **pfb2pfa** — Converts Type 1 PostScript font (binary MS-DOS) to ASCII-readable.
- **pk2bm** — Converts a TeX pkfont font file to a bitmap (ASCII file).
- **ppm2tiff** — Converts a PPM image file to a TIFF format.
- **ps2ascii** — Converts PostScript or PDF files to ASCII text.
- **ps2epsi** — Converts a PostScript file to Encapsulated PostScript (EPSI). Some word processing and graphic programs can read EPSI. Output is often low quality.
- **ps2pdf** — Converts PostScript file to Portable Document Format (PDF).
- **ps2pk** — Converts a Type 1 PostScript font to a TeX pkfont.
- **pstopext** — Converts a PostScript file to ASCII text. pstopext is similar to ps2ascii, but handles font encoding and kerning better than ps2ascii. pstopext doesn’t convert PDFs.
- **ras2tiff** — Converts a Sun raster file to a TIFF format.
- **texi2html** — Converts a Texinfo file to HTML.
- **tiff2bw** — Converts an RGB or Palette color TIFF image to a grayscale TIFF image.
- **tiff2ps** — Converts a TIFF image to PostScript.
- **unix2dos** — Converts a UNIX (Linux) text file to a DOS text file.

### Creating DocBook Documents

Documentation projects often need to produce documents that are output in a variety of formats. For example, the same text that describes how to use a software program may need to be output as a printed manual, an HTML page, and a PostScript file. The standards that have embraced most recently by the Linux community for creating what are referred to as structured documents are SGML, XML, and DocBook.

### Understanding SGML and XML

Standard Generalized Markup Language (SGML) was created to provide a standard way of marking text so that it could be output later in a variety of formats. Because SGML markup is done with text tags, create SGML documents using any plain-text editor. Document consist of the text of your document and tags that identify each type of information in the text.

Unlike markup languages such as Groff and HTML, SGML markup is not intended to enforce a particular look when you are creating the document. So, for example, instead of marking a piece of text as being bold or italic, you would identify it as an address, paragraph, or a name. Later, a style sheet would be applied to the document to take the tagged text and assign a look and presentation.

Because SGML consists of many tags, to simplify producing documents based on SGML other projects have cropped up to better focus the ways in which SGML is used. In particular, the Extensible Markup Language (XML) was created to offer a manageable subset of SGML that would be specifically tailored to work well with Web-based publishing.

So far in describing SGML and XML, I have only referred to the frameworks that are used to produce structured documents. Specific documentation projects need to create and, to some extent, enforce specific markup definitions for the type of documents they need to produce.
