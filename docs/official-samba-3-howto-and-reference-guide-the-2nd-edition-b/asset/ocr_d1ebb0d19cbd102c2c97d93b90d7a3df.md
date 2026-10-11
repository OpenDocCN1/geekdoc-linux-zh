+   • Counting the pages of the job to insert the accounting information into the `/var/log/cups/page.log`.

# 21.5.6 pstraster

*pstraster* is at the core of the CUPS filtering system. It is responsible for the first stage of the rasterization process. Its input is of MIME type `application/vnd.cups-postscript`; its output is `application/vnd.cups-raster`. This output format is not yet meant to be printable. Its aim is to serve as a general-purpose input format for more specialized raster *drivers* that are able to generate device-specific printer data. This is shown in Figure 21.6.

![](bbox=[0.05, 0.3, 0.95, 0.53])

CUPS raster is a generic raster format with powerful features. It is able to include per-page information, color profiles, and more, to be used by the downstream raster drivers. Its MIME type is registered with IANA and its specification is, of course, completely open. It is designed to make it quite easy and inexpensive for manufacturers to develop Linux and UNIX raster drivers for their printer models should they choose to do so. CUPS always takes care of the first stage of rasterization so these vendors do not need to care about Ghostscript complications (in fact, there are currently more than one vendor financing the development of CUPS raster drivers). This is illustrated in Figure 21.7.

CUPS versions before version 1.1.15 shipped a binary (or source code) standalone filter, named *pstraster*. *pstraster* which was derived from GNU Ghostscript 5.50 and could be installed instead of and in addition to any GNU or AFPL Ghostscript package without conflicting.

Since version 1.1.15, this feature has changed. The functions for this filter have been integrated back into Ghostscript (now based on GNU Ghostscript version 7.05). The *pstraster* filter is now a simple shell script calling **gs** with the `--DEVICE=cups` parameter. If your Ghostscript fails when this command is executed: `gs -h | grep cups`, you might not be able to print, update your Ghostscript.

# 21.5.7 imagetops and imageraster

In the section about predilters, we mentioned the predfilter that generates PostScript from image formats. The *imagetops* filter is used to convert, directly from image to raster.