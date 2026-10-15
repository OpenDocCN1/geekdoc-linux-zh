```
printing = cups
printcap name = cups
```

To enable CUPS to work with Samba, you have to link the smbspool to the CUPS smb spool directory:

```
ln -s /usr/bin/smbspool  /usr/cups/backend/smb
```

To access a printer connected to a Linux or Unix system running LPRng, use the lpd protocol to specify its location. In the following example, the printer mylaser is connected to the Linux host rabbit.mytrek.com:

```
lpd://rabbit.mytrek.com/mylaser
```

# CUPS Printer Classes

CUPS features a way to let you select a group of printers to print a job instead of selecting just one. That way, if one printer is busy or down, another printer can be automatically selected to perform the job. Such groupings of printers are called classes. Once you have installed your printers, you can then group them into different classes. For example, you may want to group all inkjet printers into one class and laser printers into another, or you may want to group printers connected to one specific printer server in their own class. To create a class, select Classes on the Administration page and enter the name of the class. You can then add printers to it.

# CUPS Configuration

CUPS configuration files are placed in the /etc/cups directory. These files are listed in Table 25-1. The classes.conf, printers.conf, and client.conf files can be managed by the Web interface. The printers.conf file contains the configuration information for the different printers you have installed. Any of these files can be edited manually, if you wish.

# cupsd.conf

The CUPS server is configured with the cupsd.conf file located in /etc/cups. You must edit configuration options manually; the server is not configured with the Web interface. Your installation of CUPS installs a commented version of the cupsd.conf file with each option listed, though most options will be commented out. Commented lines are preceded with a # symbol. Each option is documented in detail. The server configuration uses an Apache Web server syntax consisting of a set of directives. As with Apache, several of these directives can group other directives into blocks.

| Filename | Description |
|---|---|
| classes.conf | Configurations for different local printer classes |
| client.conf | Lists specific options for specified clients |
| cupsd.conf | Configures the CUPS server, cupsd |
| printers.conf | Printer configurations for available local printers |