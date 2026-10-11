# **Figure 21.17** Filtering Chain 1.

CUPS in and of itself has this (general) filter chain (*italic* letters are *file-formats* or MIME types, other are filters (this is true for pre-1.1.15 of pre-4.3 versions of CUPS and ESP PrintPro):

![](bbox=[0.04, 0.17, 0.91, 0.535])

ESP PrintPro has some enhanced “rastertosomething” filters as compared to CUPS, and also a somewhat improved “*pstoraster*” filter.

NOTE: Gimp-Print and some other 3rd-Party-Filters (like TurboPrint) to CUPS and ESP PrintPro plug-in where *rastertosomething* is noted.

If the error is “*Tree connect failed: NT_STATUS_BAD_NETWORK_NAME*”, you may have forgotten to create the */etc/samba/drivers* directory.

# **21.19.3  “cupsaddslmb” or “rpcclient addrivers” Emit Error**

If cupsaddslmb, or rpcclient addrivers emit the error message WERR_BAD_PASSWORD, refer to Section 21.19.2.

# **21.19.4  “cupsaddslmb” Errors**

The use of “cupsaddslmb” gives “No PPD file for printer...” message while PPD file is present. What might the problem be?