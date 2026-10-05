# Installing a printer driver from the command line

As you may have guessed already, some of these steps are hard to replicate without Windows, especially the setting printer defaults. But if you want to set up hundreds of printers on a Samba server, you may want to try to do it from the command line all the. Command-line configuration works particularly well for PostScript printers because the Windows PostScript printer driver works correctly without default configuration information.

If you made a note of the files required by a particular driver, you can install the driver from the command line. First, copy the files required to the [print]$ share:

```
$ cd ~/mydriver
$ smclient -U printdam //samba-server/print$ -c "mput *"
```

Next, assign the driver to a particular printer. Let's assume you have a simple Post-Script printer with a custom PPD file:

```
$ rpclient -U printdam -c "\"
addriver\"Windows NT x86\"Our Custom PS:\nPSCRIPT.DLL:CUSTOM.PPD:PSSUI.DLL:PSCRIPT.HLP:NULL:NULL:PSCRIPT.NTF""\nsamba-server
```

The backslashes at the ends of lines allow the command to be split onto multiple lines for clarity; you can omit these and enter the command on one line if you prefer. The backslashes before double quotes distinguish the nested sets of quotes.

The long string in the example above contains the information listed in the property of the printer driver that is seen when the printer driver is being installed from Windows:

+   * Long printer name
* Driver filename
* Data filename
* Configuration filename
* Help filename
* Language monitor name (set this to NULL if you have none)
* Default data type (set this to NULL if there is none)
* Comma-separated list of additional files

To configure a printer to use one of the uploaded drivers,

```
$ rpclient -U printdam -c "\"Our Custom PS\"" samba-server
```

# 30.8 DEBUGGING SAMBA

Samba usually runs without requiring much attention. However, if you have a problem, you can consult two primary sources of debugging information: the log