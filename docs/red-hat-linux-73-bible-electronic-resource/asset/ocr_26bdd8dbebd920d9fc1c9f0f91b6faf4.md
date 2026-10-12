Because of the ongoing development effort, new scanners are being supported all the time. You can find a current list of supported scanners at `www.mostang.com/sane/sane-backends.html`. As for applications, these are currently available with Red Hat Linux:

+   - **xsane** — This is an X-based graphical front end for SANE scanners; *xsane* can work as a GIMP plug-in or as a separate application. It supports 8-bit output in JPG, TIFF, PNG, PostScript, and PNM formats. There is experimental 16-bit support for PNM (ASCII), PNG, and raw formats. Figure 6-15 shows the *xsane* window.

![](bbox=[0.08, 0.24, 0.33, 0.48])

+   - **xscanimage** — Another X-based window used to preview and scan images from a Linux scanner or digital camera. Starting *xscanimage* from the command line lets you save images in PBM (black-and-white), PGM (grayscale), or PPM (color). When used as a GIMP plug-in, GIMP processes the images.
+   - **scanimage** — This is a command-line interface for obtaining scanned images. It supports the same formats as *xscanimage*. The command acquires the scanned image, and then directs the data to standard output (so you can send it to a file or pipe it to another program).
+   - **xcam** — This graphical interface lets you grab continuous images from a video camera interface on your system.

Because of the architecture of SANE scanner drivers, it is possible to separate scanner drivers from scanner applications. This makes it possible to share scanners and video cameras across a network.

# # Summary

In recent times, modern GUI-based publishing tools have augmented the text-based publishing tools that have always been available with Red Hat Linux (and other UNIX systems).
Publishing tools that come with Red Hat Linux include Groff (which implements traditional