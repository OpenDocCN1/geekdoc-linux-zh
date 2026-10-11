```
root# rpcclient SAMBA-CUPS -U root%secret -c 'enumprinters'
cmd = enumprinters
flags: [0x800000]
name: [\\SAMBA-CUPS\dm9110]
description: [\\SAMBA-CUPS\dm9110,Heidelberg Digimaster 9110 (PS),\
110ppm HiVolume DANKA Stuttgart]
comment: [110ppm HiVolume DANKA Stuttgart]
[...]
```

```
root# rpcclient SAMBA-CUPS -U root%secret -c 'setdriver dm9110 mydrivername'
cmd = setdriver dm9110 mydrivername
Successfully set dm9110 to mydrivername.
```

```
root# rpcclient SAMBA-CUPS -U root%secret -c 'enumprinters'
cmd = enumprinters
flags: [0x800000]
name: [\\SAMBA-CUPS\dm9110]
description: [\\SAMBA-CUPS\dm9110,mydrivername,\
110ppm HiVolume DANKA Stuttgart]
comment: [110ppm HiVolume DANKA Stuttgart]
[...]
```

It may not be easy to recognize that the first call to `enumprinters` showed the “dm9110” printer with an empty string where the driver should have been listed (between the two commas in the description field). After the `setdriver` command succeeds, all is well.

# 20.8.3 Adding New Printers with the Windows NT APW

By default, Samba exhibits all printer shares defined in `smb.conf` in the **Printers** folder. Also located in this folder is the Windows NT Add Printer Wizard icon. The APW will be shown only if:

+   • The connected user is able to successfully execute an `OpenPrinterEx(\\server)` with administrative privileges (i.e., `root` or `printer admin`).