Someone wanting to use Linux as a publishing platform is generally interested in two issues about scanners: which scanners are supported and which applications are available to use the scanners. In general, more SCSI scanners are supported than parallel scanners.

Because of the ongoing development effort, new scanners are being supported all the time. You can find a current list of supported scanners at www.sane-project.org/sane-supported-devices.html, with USB scanners listed at www.buzzard.me.uk/jonathan/scanners-usb.html. As for applications, these are currently available with Fedora:

+   - **xsane** — This is an X-based graphical front end for SANE scanners; xsane can work as a GIMP plug-in or as a separate application (from the red hat menu, select Graphics → Scanning). It supports 8-bit output in JPG, TIFF, PNG, PostScript, and PNM formats. There is experimental 16-bit support for PNM (ASCII), PNG, and raw formats.
+   - **scanimage** — This is a command-line interface for obtaining scanned images. It supports the same formats as xsaneimage. The command acquires the scanned image, and then directs the data to standard output (so you can send it to a file or pipe it to another program).

In addition to these applications, the OpenOffice.org suite supports SANE. Because of the architecture of SANE scanner drivers, it is possible to separate scanner drivers from scanner applications. This makes it possible to share scanners across a network.

# Summary

In recent times, modern GUI-based publishing tools have augmented the text-based publishing tools that have always been available with Fedora (and other Red Hat Linux systems). Powerful open-source publishing tools such as OpenOffice.org are becoming competitive with commercial office suites. Traditional publishing tools such as Groff (which implements traditional troff/nroff text processing) and LaTeX (a TeX macro interface that is particularly suited for scientific and mathematical publishing) are still available with Fedora.