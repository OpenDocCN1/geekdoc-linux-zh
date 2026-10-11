Not all of the mentioned backends may be present on your system or usable (depending on your hardware configuration). One test for all available CUPS backends is provided by the *lpinfo* utility. Used with the *-v* parameter, it lists all available backends:

```
$ lpinfo -v
```

# 21.5.10 The Role of cupsomatic/foomatic

*cupsomatic* filters may be the most widely used on CUPS installations. You must be clear that these were not developed by the CUPS people. They are a third-party add-on to CUPS. They utilize the traditional Ghostscript devices to render jobs for CUPS. When troubleshooting, you should know about the difference. Here the whole rendering process is done in one stage, inside Ghostscript, using an appropriate device for the target printer. *cupsomatic* uses PPDs that are generated from the Foomatic Printer & Driver Database at Linuxprinting.org.

You can recognize these PPDs from the line calling the *cupsomatic* filter:

```
*cupsFilter: "application/vnd.cups-postscript 0 cupsomatic"
```

You may find this line among the first 40 or so lines of the PPD file. If you have such a PPD installed, the printer shows up in the CUPS Web interface with a *foomatic* name/part for the driver description. *cupsomatic* is a Perl script that runs Ghostscript with all the complicated command-line options autoconstructed from the selected PPD and command line options give to the print job.

However, *cupsomatic* is now deprecated. Its PPDs (especially the first generation of them, still in heavy use out here) are not meeting the Adobe specifications. You might also suffer difficulties when you try to download them with “Point n’Print” to Windows clients. A better and more powerful successor is now in a stable beta-version: it is called *foomatic-rip*. To use *foomatic-rip* as a filter with CUPS, you need the new type of PPDs, which have a similar but different line:

```
*cupsFilter: "application/vnd.cups-postscript 0 foomatic-rip"
```

The PPD-generating engine at Linuxprinting.org has been revamped. The new PPDs comply with the Adobe spec. They also provide a new way to specify different quality levels (hi-res photo, normal color, grayscale, and draft) with a single click, whereas before you could have required five or more different selections (media type, resolution, inktype, and dithering algorithm). There is support for custom-size media built in. There is support to switch print options from page to page in the middle of a job. And the best thing is that the new *foomatic-rip* works seamlessly with all legacy spoolers too (like: LPRng, BSD-LPD, PDQ, PPR, and so on), providing for them access to use PPDs for their printing.