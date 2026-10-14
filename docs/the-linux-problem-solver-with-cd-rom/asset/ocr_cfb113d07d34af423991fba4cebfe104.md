:lf=/var/spool/lpd/smb/log:pw#80:\
:lf=/usr/local/lib/filters/smbprint:

Again, you'll need to create a new null device:

```
# mknod spoolidir/null c 1 3
```

where spoolidir is the one sd specifies in the printcap (as in /var/spool/lpd/smb above).

Now you'll need to set up the filter properly. The filter is probably not installed in /usr/local/lib/filters. In Red Hat 6.1, for example, you'll find it in /usr/bin, and if you installed SAMBA from source, it won't be installed by default anyway (it's in the source, in the subdirectory examples/printing).

The filter is just a shell script and needs a .config file in the spool directory of the printer; that would be /var/spool/lpd/smb in the example above.

The .config file looks like this:

```
server=SERVER
service=PRINTER
password="PASSWORD"
```

SERVER, PRINTER, and PASSWORD are the details of the SMB printer (you probably won't need a password for printing, so you can omit that line). You may need to change the last line of the file to reflect where you installed SAMBA (the example in the source assumes you put it in /usr/local/samba/bin).

> NOTE
> Red Hat's smbprint differs from the example in that it sets the SMB log file to /dev/null instead of /tmp/smb-print.log, and it gives the proper Red Hat location of smbclient

You can use the smbclient program to look up the shares available on a machine, as in this example:

```
$ smbclient -L printserver
Password:
Domain=[FOO] OS=[Unix] Server=[Samba 1.9.18p10]
```

| Sharename | Type | Comment |
|----------|------|---------|
| printers | Printer | All Printers |
| hp160b | Printer | HP LaserJet 5Si in room 160b |
| ... | ... | ... |

For this to work, the printer must support PostScript. If it doesn't, you'll need to run the file through Ghostscript before sending it off.