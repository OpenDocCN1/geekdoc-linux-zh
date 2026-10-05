# PDF conversion

LaTeX → PDF
With the LaTeX command latexpdf you create a *.pdf file from a *.tex file instead of a *.dvi file. While the application of the command is extremely simple, the results for complex documents using various fonts and macro packages (such as the *.tex files of this) are available only to a very limited extent. In some cases, the PDF files could not even be properly displayed by acroload. latexpdf is part of the supply only unless teTeX 0.9 and is therefore missing in many older distributions.

PS → PDF
ps2pdf source.target creates a PDF file from an arbitrary PostScript file. The command is based on GhostScript. The results are only usable if the PostScript exclusively contains texts in the Courier, Times and Helvetica fonts. Otherwise, bitmaps are used for character representation, which both reduces the quality and makes file size grow hugely. Furthermore, the resulting PDF file is not even compressed.

PDF → PS
The opposite way is taken by pdf2ps source.pdf target.ps. This command resorts to Ghostscript.

# Graphics conversion

XV
The most popular tool in the Unix world for conversion of graphics files between different formats is without any doubt xv. You can use it to read graphics files in the most varied formats and store them in a different format. At the same time, it offers various operations for image processing (rotate, mirror, and so on) and color manipulation (brightness, contrast). Furthermore xv can be used to draw screens, that is, to store a window or the whole screen in a graphics file of arbitrary format. Last, but not least, you can use xv as a file manager (VISUAL SCHNAUZER).

Unlike other Linux components, xv is shareware. Commercial use is only permitted after licensing. The license agreement is displayed by clicking on the LICENSE button.
A few words about handling xv: when it starts up, a colorful logo is displayed. The actual control window only appears after clicking on the logo with the right mouse button. Through the control window, you can load a file. When xv recognizes the graphics format, it displays the file in a graphics window.
Now, you can carry out some elementary processing steps directly via buttons in the control window. Should you want to change brightness, contrast or other color settings, clicking on WINDOWS COLOR EDITOR provides you with a separate window with countless setting possibilities.