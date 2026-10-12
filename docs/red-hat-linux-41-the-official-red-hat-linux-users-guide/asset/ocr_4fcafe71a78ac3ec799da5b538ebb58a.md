# ## 3.3 Installing the Miniloader MILO

The easiest method of booting Red Hat Linux/Alpha is through the Linux Miniloader, MILO. You may either load MILO directly from your system's firmware, or use the ARC console to load MILO as an alternate OS. Details on these procedures are in the MILO FAQ, which is available as Appendix E.

The full MILO tree is available on the CD in the *milo* directory. It contains the latest documentation and MILO images available when this CD was manufactured. However, later versions of MILO are regularly made available at *gatekeeper.dec.com*. The *images/arc* directory also contains floppy disk images that can be used with the ARC console to boot directly into MILO. They contain MILO and **load.exe**, as well as a flashable version of MILO and the flash management utility for the platforms which support flashing MILO. If you have trouble with MILO, the first thing to try is a newer MILO.

If MILO is not supported on your machine, you need to boot the floppy or the CD directly from the SRM console. Information on doing this is available from the Red Hat Software web site at `http://www.redhat.com/linux-info/alpha/faq`.

# ## 3.4 Installing Red Hat Linux/Alpha

# ### 3.4.1 Making a Boot disk

The first step in installing Red Hat Linux/Alpha is creating a boot disk; which boot disk to use depends on the hardware you have. A variety of boot disk images are available on the Red Hat Linux/Alpha CD in the *images* directory, along with a README containing more information about the various images which are available.

Available boot images include:

+   1. `cab.img` (AlphaPC64, Cabriole)
+   2. `noname.img` (AxpPCI33, Noname, Universal Desktop Box)
+   3. `eb64p.img` (EB64+, Aspen Timberlines)