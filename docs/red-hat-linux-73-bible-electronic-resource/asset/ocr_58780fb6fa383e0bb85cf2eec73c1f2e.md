+   - **ps2epsi** — Converts a PostScript file to Encapsulated PostScript (EPSI). Some word processing and graphic programs can read EPSI. Output is often low quality.
+   - **ps2pdf** — Converts PostScript file to Portable Document Format (PDF).
+   - **ps2pk** — Converts a Type 1 PostScript font to a TeX pkfont.
+   - **pstopext** — Converts a PostScript file to ASCII text. pstopext is similar to ps2ascii, but handles font encoding and kerning better than ps2ascii. pstopext doesn’t convert PDFs.
+   - **ras2tiff** — Converts a Sun raster file to a TIFF format.
+   - **texi2html** — Converts a Texinfo file to HTML.
+   - **tiff2bw** — Converts an RGB or Palette color TIFF image to a grayscale TIFF image.
+   - **tiff2ps** — Converts a TIFF image to PostScript.
+   - **unix2dos** — Converts a UNIX (Linux) text file to a DOS text file.

# ### Creating DocBook Documents

Documentation projects often need to produce documents that are output in a variety of formats. For example, the same text that describes how to use a software program may need to be output as a printed manual, an HTML page, and a PostScript file. The standards that have embraced most recently by the Linux community for creating what are referred to as structured documents are SGML, XML, and DocBook.

# ## Understanding SGML and XML

Standard Generalized Markup Language (SGML) was created to provide a standard way of marking text so that it could be output later in a variety of formats. Because SGML markup is done with text tags, create SGML documents using any plain-text editor. Document consist of the text of your document and tags that identify each type of information in the text.

Unlike markup languages such as Groff and HTML, SGML markup is not intended to enforce a particular look when you are creating the document. So, for example, instead of marking a piece of text as being bold or italic, you would identify it as an address, paragraph, or a name. Later, a style sheet would be applied to the document to take the tagged text and assign a look and presentation.

Because SGML consists of many tags, to simplify producing documents based on SGML other projects have cropped up to better focus the ways in which SGML is used. In particular, the Extensible Markup Language (XML) was created to offer a manageable subset of SGML that would be specifically tailored to work well with Web-based publishing.

So far in describing SGML and XML, I have only referred to the frameworks that are used to produce structured documents. Specific documentation projects need to create and, to some extent, enforce specific markup definitions for the type of documents they need to produce.