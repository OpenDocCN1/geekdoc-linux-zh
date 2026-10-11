
## 21.8 Network PostScript RIP

This section discusses the use of CUPS filters on the server configuration where clients make use of a PostScript driver with CUPS-PPDs.

PPDs can control all print device options. They are usually provided by the manufacturer if you own a PostScript printer; that is, PPD files are always a component of PostScript printer drivers on MS Windows or Apple Mac OS systems. They are ASCII files containing user-selectable print options, mapped to appropriate PostScript, PCL or Pjl commands for the target printer. Printer driver GUI dialogs translate these options "on the fly" into buttons and drop-down lists for the user to select.

CUPS can load, without any conversions, the PPD file from any Windows (NT is recommended) PostScript driver and handle the options. There is a Web browser interface to the print options (select <http://localhost:631/printers/> and click on one **Configure Printer** button to see it) or a command-line interface (see `man lpoptions` or see if you have `lphpel` on your system). There are also some different GUI front-ends on Linux/UNIX, which can present PPD options to users. PPD options are normally meant to be evaluated by the PostScript RIP on the real PostScript printer.

### 21.8.1 PPDs for Non-PS Printers on UNIX

CUPS does not limit itself to “real” PostScript printers in its use of PPDs. The CUPS developers have extended the scope of the PPD concept to also describe available device and driver options for non-PostScript printers through CUPS-PPDs.

This is logical, because CUPS includes a fully featured PostScript interpreter (RIP). This RIP is based on Ghostscript. It can process all received PostScript (and additionally many other file formats) from clients. All CUPS-PPDs geared to non-PostScript printers contain an additional line, starting with the keyword `*cupsFilter`. This line tells the CUPS print system which printer-specific filter to use for the interpretation of the supplied PostScript. Thus CUPS lets all its printers appear as PostScript devices to its clients, because it can act as a PostScript RIP for those printers, processing the received PostScript code into a proper raster print format.

### 21.8.2 PPDs for Non-PS Printers on Windows

CUPS-PPDs can also be used on Windows clients, on top of a “core” PostScript driver (now recommended is the CUPS PostScript Driver for Windows NT/2000s/XP; you can also use the Adobe one, with limitations). This feature enables CUPS to do a few tricks no other spooler can do:

- Act as a networked PostScript RIP handling print files from all client platforms in a uniform way.
- Act as a central accounting and billing server, since all files are passed through the postps filter and are therefore logged in the CUPS `page.log` file. *Note*: this cannot happen with “raw” print jobs, which always remain unfiltered per definition.
- Enable clients to consolidate on a single PostScript driver, even for many different target printers.

Using CUPS PPDs on Windows clients enables them to control all print job settings just as a UNIX client can do.

## 21.9 Windows Terminal Servers (WTS) as CUPS Clients

This setup may be of special interest to people experiencing major problems in WTS environments. WTS often need a multitude of non-PostScript drivers installed to run their clients’ variety of different printer models. This often imposes the price of much increased instability.

### 21.9.1 Printer Drivers Running in “Kernel Mode” Cause Many Problems

Windows NT printer drivers, which run in “kernel mode”, introduce a high risk for the stability of the system if the driver is not really stable and well-tested. And there are a lot of bad drivers out there! Especially notorious is the example of the PCL printer driver that had an additional sound module running to notify users via soundcard of their finished jobs. Do I need to say that this one was also reliably causing “blue screens of death” on a regular basis?

PostScript drivers are generally well-tested. They are not known to cause any problems, even though they also run in kernel mode. This might be because until now there have been only two different PostScript drivers: the one from Adobe and the one from Microsoft. Both are well-tested and are as stable as you can imagine on Windows. The CUPS driver is derived from the Microsoft one.

### 21.9.2 Workarounds Impose Heavy Limitations

In an attempt to work around problems, site administrators have resorted to restricting the allowed drivers installed on their WTS to one generic PCL and one PostScript driver. This, however, restricts the number of printer options available for clients to use. Often they can’t get out more than simplex prints from one standard paper tray, while their devices could do much better if driven by a different driver!

### 21.9.3 CUPS: A “Magical Stone”?

Using a PostScript driver, enabled with a CUPS-PPD, seems to be a very elegant way to overcome all these shortcomings. There are, depending on the version of Windows OS you use, up to three different PostScript drivers now available: Adobe, Microsoft, and CUPS PostScript drivers. None of them is known to cause major stability problems on WTS (even if used with many different PPDs). The clients will be able to (again) choose paper trays, duplex printing, and other settings. However, there is a certain price for this too: a CUPS server acting as a PostScript RIP for its clients requires more CPU and RAM than you just acting as a “raw spooling” device. Plus, this setup is not yet widely tested, although the first feedbacks look very promising.

### 21.9.4 PostScript Drivers with No Major Problems, Even in Kernel Mode

More recent printer drivers on W200x and XP no longer run in kernel mode (unlike Windows NT). However, both operating systems can still use the NT drivers, running in kernel mode (you can roughly tell which is which as the drivers in subdirectory “2” of “W32X86” are “old” ones). As was said before, the Adobe as well as the Microsoft PostScript drivers are not known to cause any stability problems. The CUPS driver is derived from the Microsoft one. There is a simple reason for this: the MS DDK (Device Development Kit) for Windows NT (which used to be available at no cost to licensees of Visual Studio, “Classical Printing NT” where used to be available at no cost to licensees of Visual Studio 20.) includes the source code of the Microsoft driver, and licensees of Visual Studio are allowed to use and modify it for their own driver development efforts. This is what the CUPS people have done. The license does not allow them to publish the whole of the source code. However, they have released the “diff” under the GPL, and if you are the owner of an “MS DDK for Windows NT,” you can check the driver yourself.

## 21.10 Configuring CUPS for Driver Download

As we have said before, all previously known methods to prepare client printer drivers on the Samba server for download and Point`print` coexistence of Windows workstations are working with CUPS, too. These methods were described in Chapter 20, “Classical Printing Support”. In reality, this is a pure Samba business and relates only to the Samba-Windows client relationship.

### 21.10.1 cupsaddsm: The Unknown Utility

The `cupsaddsm` utility (shipped with all current CUPS versions) is an alternative method to transfer printer drivers into the Samba [p\*r\*i\*n\*t\*s] share. Remember, this share is where clients expect drivers deposited and set up for download and installation. It makes the sharing of any (or all) installed CUPS printers quite easy: `cupsaddsm` can use the Adobe PostScript driver as well as the newly developed CUPS PostScript driver for Windows NT/W200x/XP. `cupsaddsm` does not work with arbitrary vendor printer drivers, but only with the exact driver files that are named in its man page.

The CUPS printer driver is available from the CUPS download site. Its package name is cups-samba-[version].tar.gz. It is preferred over the Adobe drivers because it has a number of advantages:

- It supports a much more accurate page accounting.
- It supports banner pages and page labels on all printers.
- It supports the setting of a number of job IPP attributes (such as job priority, page label, and job billing).
