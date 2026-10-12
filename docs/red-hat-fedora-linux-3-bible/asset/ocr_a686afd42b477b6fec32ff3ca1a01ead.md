| Description | Drive Letter or Name | Linux Directory or Output Location | Linux Device Name (If Applicable) |
| --- | --- | --- | --- |
| Serial ports | COM1<br>COM2<br>COM3<br>COM4 |  | /dev/ttyS0<br>/dev/ttyS1<br>/dev/ttyS2<br>/dev/modem |
| Parallel ports | LPT1 |  | /dev/lp0 |
| Print spooler | LPT1 | Pipes printer jobs to the lpr command (lpr) |  |
| WineLook | Win95 (how the system appears to apps: Win31, Win98, or the default Win95) |  |  |

Within the $HOME/.wine/drive_c directory (that is, your C: drive), you should see some things that are familiar to you if you are coming from an older Windows environment: Program Files and windows directories.

Assuming that the basic directory structure is okay with you, you may still want to consider changing a few items. For example, you may want to change the command to print documents (set in the /etc/wine/config file) to something other than the "lpr" command to use a particular printer or add some Linux printing options.

> NOTE: For details on configuring the wine.conf file, see the Wine User Guide. That guide (wine-user.pdf) is stored in the /usr/share/doc/wine* directory when you install the wine RPM for Fedora Core.

For Windows applications that are included on CD or DVD, you can try installing them by simply running the setup program on that medium with the wine command. So, with a CD containing the application you want to install inserted and mounted, you would run a command like the following:

```
# wine d:\Setup.exe
```

The application will run, just as it would in Windows, to install the application to your hard disk.