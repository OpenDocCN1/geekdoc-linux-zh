# ## 21.8 Network PostScript RIP

This section discusses the use of CUPS filters on the server configuration where clients make use of a PostScript driver with CUPS-PPDs.

PPDs can control all print device options. They are usually provided by the manufacturer if you own a PostScript printer; that is, PPD files are always a component of PostScript printer drivers on MS Windows or Apple Mac OS systems. They are ASCII files containing user-selectable print options, mapped to appropriate PostScript, PCL or Pjl commands for the target printer. Printer driver GUI dialogs translate these options "on the fly" into buttons and drop-down lists for the user to select.

CUPS can load, without any conversions, the PPD file from any Windows (NT is recommended) PostScript driver and handle the options. There is a Web browser interface to the print options (select <http://localhost:631/printers/> and click on one **Configure Printer** button to see it) or a command-line interface (see `man lpoptions` or see if you have `lphpel` on your system). There are also some different GUI front-ends on Linux/UNIX, which can present PPD options to users. PPD options are normally meant to be evaluated by the PostScript RIP on the real PostScript printer.

# ### 21.8.1 PPDs for Non-PS Printers on UNIX

CUPS does not limit itself to “real” PostScript printers in its use of PPDs. The CUPS developers have extended the scope of the PPD concept to also describe available device and driver options for non-PostScript printers through CUPS-PPDs.

This is logical, because CUPS includes a fully featured PostScript interpreter (RIP). This RIP is based on Ghostscript. It can process all received PostScript (and additionally many other file formats) from clients. All CUPS-PPDs geared to non-PostScript printers contain an additional line, starting with the keyword `*cupsFilter`. This line tells the CUPS print system which printer-specific filter to use for the interpretation of the supplied PostScript. Thus CUPS lets all its printers appear as PostScript devices to its clients, because it can act as a PostScript RIP for those printers, processing the received PostScript code into a proper raster print format.

# ### 21.8.2 PPDs for Non-PS Printers on Windows

CUPS-PPDs can also be used on Windows clients, on top of a “core” PostScript driver (now recommended is the CUPS PostScript Driver for Windows NT/2000s/XP; you can also use the Adobe one, with limitations). This feature enables CUPS to do a few tricks no other spooler can do:

+   - Act as a networked PostScript RIP handling print files from all client platforms in a uniform way.

+   - Act as a central accounting and billing server, since all files are passed through the postps filter and are therefore logged in the CUPS `page.log` file. *Note*: this cannot happen with “raw” print jobs, which always remain unfiltered per definition.