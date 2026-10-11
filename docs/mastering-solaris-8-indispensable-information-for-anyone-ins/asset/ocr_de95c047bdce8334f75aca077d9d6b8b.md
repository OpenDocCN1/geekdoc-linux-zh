Whereas the `lpsched` daemon manages the scheduling for local print requests, it is the `lpNet` daemon that initiates network print requests. A print client and print server must have one, but can have more, `lpNet` daemons running on a system. Your system starts the `lpNet` daemon when it boots. When you use the `lpshut` command to stop the `lpsched` daemon, it also shuts down any `lpNet` daemons that are running. When you restart the `lpsched` daemon, the `lpNet` daemons also restart. The `lpNet` daemon uses the Service Access Facility—`sacadm(1M)` and `pmadm(1M)`—to work with a configured port monitor and provide the registration service so that it can listen to incoming network requests for printer services. Beginning with Solaris 2.6, it is the `lnetd` Internet services super daemon that provides network print scheduling. When the daemon hears a request over the port, it starts in-`npd`, which examines the print request and loads `bsd_lpsched`, which then has in-`lpd` pass the request through to `lpsched` for local printing.

# Spooling

A spooling space is set aside on a system for a local printer and on a print server for network printing to store and process print files prior to execution. When the printer requests the next print job in the print queue, the file in the spooler directory is sent to the print filter and then the result is transmitted to the printer as a set of control codes. Files for the spooler are commonly stored in the `/var/spool/lp` directory and deleted once they are printed.

You can see what files are spooled locally in the print queue by clicking the Print Manager control on the Personal Printers subpanel of the CDE front panel. Figure 10.3 shows the queue for a local printer.

Pay attention to the amount of free space that a disk has when you designate it to be a print server. Print jobs can often be quite large, with graphics consuming a lot of disk space. It isn't uncommon to have a large spooling directory fill 600MB of disk space. You may need to make more disk space available for use in heavy print situations.

SunSoft clients do not maintain a permanent print queue, only print servers do. The client will create a temporary print queue when the print server is unavailable, but jobs in that print queue are sent to the print server's queue once the server comes back online.

If you need to move the files from one print server to another because a printer has become unavailable, you can use the `lpmove` command. The command takes the following form (this command moves the print jobs 120 and 125 to the print server of the Xerox3 printer):

```
lpmove flash-120 flash-125 xerox3
```

To move all documents from one queue to another, specify the following:

```
lpmove flash xerox3
```