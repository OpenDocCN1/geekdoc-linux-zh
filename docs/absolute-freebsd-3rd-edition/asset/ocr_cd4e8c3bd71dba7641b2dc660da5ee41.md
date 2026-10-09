access. Make an entry in `/etc/printcap` following this template. Pay special attention to the colons and backslashes—they’re absolutely vital.

```
```
1lp/printername:\n    2:sh=:\n    3:rm=printservername:\n    4:sd=/var/spool/output/lpd/printername:\n    5:lf=/var/log/lpd-errs:\n    6:rp=printername:
```
```

Our first line shows the printer’s name 1. If you print from LibreOffice or a graphical web browser, these names will show up as printer options. Each printer can have any number of names, separated by the pipe symbol (|). The default printer on any Unix-like system is called lp, so list that as one of the names for your preferred printer. One other name should be the name used by the print server for your printer (for example, 3rdFloorPrinter). Be warned, Microsoft print servers frequently share one printer under several different names and use different names to handle printing differently. If you find this to be the case on your network, be sure to choose the PostScript name.7

By default, lpd(8) precedes each print job with a page listing the job name, number, host, and other information. Unless you’re in an environment with a single massive shared printer, this is probably a waste of paper. The `:sh:\` entry 2 suppresses this page.

The rm (remote machine) variable 3 provides the hostname of the print server. You must be able to ping this server by the name you give here. If the print server is part of the printer, give the printer’s hostname here.

Each printer requires a unique spool directory 4, where the local print daemon can store documents in transit to the print server. This directory must be owned by user root and group daemon.

Unlike spool directories, which must be different, printers can share a common log file 5.

Finally, specify the remote printer name 6, as the print server identifies it. If you’re connecting directly to a printer, not to a central