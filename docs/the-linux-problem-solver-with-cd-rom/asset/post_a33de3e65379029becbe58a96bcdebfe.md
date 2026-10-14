
```
# cat > spooldir/.paprc
printername
^D
```

If this doesn’t work right away, you can test a few things. First cd to the spool directory (the one containing the .paprc) and use

```
# papstatus
```

to see if you can at least talk to the printer (the papstatus command is in the bin directory of wherever you installed Netatalk). If the .paprc file doesn’t contain the right name, you’ll get an error like this one:

```
printer:LaserWriter%: NBP Lookup failed
```

Use the -p option to find the right printer. If you have no idea what it is, try the nbplkup command (in the same directory as the papstatus command; see Chapter 4 for more information on nbplkup):

```
# nbplkup :LaserWriter
```

You should get a listing of the printers offering LaserWriter service and their AppleTalk network numbers. To list a different zone, tack @zone onto the end of :LaserWriter (Netatalk’s getzones command lists the available zones). Of course, you could also use the Chooser on a Mac—the LaserWriter 8 service is the one you want.

Once you get a printer status report, such as idle, try sending the printer a PostScript file with pap:

```
# pap file.ps
```

By the way, a rather interesting option, -c, tells the printer this print job has been waiting forever, and tries to get the job in first ahead of any other jobs in the print queue.

Relevant man pages: psf (8), pap (1), nbp (1), getzones (1)

## SMB Printers

If your printer is on an SMB share on a Windows machine, you can use SAMBA’s smbclient program to print to it. The printcap will look much like the one with AppleTalk:

```
smbprinter|Printer on SMB Share:\
	:mx#0:sf:sh:\
	:sd=/var/spool/lpd/smb:\
	:lp=/var/spool/lpd/smb/null:\
:lf=/var/spool/lpd/smb/log:pw#80:\
:lf=/usr/local/lib/filters/smbprint:
```

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

## 5.4 Ghostscript for Non-PostScript Printers

Most inexpensive printers do not have built-in PostScript support. These include most inkjets and a few low-end or older laser printers. However, the computer can often interpret and rasterize the file, ultimately sending a finished bitmap to the printer. Ghostscript, developed by Aladdin Enterprises, is a popular free interpreter and rasterizer that comes with most Linux distributions and has most or all of the devices configured.

While Ghostscript supports many printers, the correct options and drivers are not always obvious and its documentation is messy, with information scattered over a number of files. Certain options—those for color inkjets in particular—significantly change output quality. For example, the defaults for an Epson Stylus Color 850 are not the best for transparencies, although the printer is capable of producing very good results (ideally you would want unidirectional printhead movement to reduce streaking and perhaps a different kind of dithering from usual).

You typically integrate Ghostscript into Linux’s print spooling system as a filter. PostScript goes in and printer-ready data comes out and goes to the printer. The filter is usually a shell script, which parses some arguments and then calls Ghostscript with some options. Here is a very simple script:

```
```sh
#!/bin/sh
/usr/bin/gs -q -dNOPAUSE -dBATCH -sOutputDevice=-- -r720x360 -sDEVICE=epson -
```
```

The heart of this is, of course, the call to Ghostscript (gs). When you customize your filter, you will probably invoke gs on the command line to avoid specifying the many parameters that a print filter requires.

To send the output of a run on foo.ps straight to the parallel port, run this:

```
```sh
# gs -q -dNOPAUSE -dBATCH -sOutputDevice=/dev/lp0 -r720x360
- -sDEVICE=epson foo.ps
```
```

### Using the uniprint Driver

You’ll generally want to call the uniprint driver as follows:

```
```sh
# gs @name.upp -q -dNOPAUSE -dBATCH -sOutputDevice=device [files]
```
```

name.upp is actually a parameter file in the Ghostscript library directory. For example, stc800.upp is a 720-by-720-dpi plain-paper mode for the Epson Stylus Color 800. The file itself is a huge listing of options that set uniprint as the driver and tweak the parameters for this particular printer.
