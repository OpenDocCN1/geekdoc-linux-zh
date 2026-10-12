Here, printing to the ns1-hp1 printer is only allowed for users on the local host (127.0.0.1). No password is needed (AuthType None). To allow access to the administration tool requires the CUPS be configured to prompt for a password (AuthType Basic).

If you change any of the settings in the cupsd.conf file, you must restart the CUPS service to have the changes take effect. As root user, type chkconfig cupsd restart.

# ## Configuring CUPS printer options

When a new printer is created from the Printer configuration window, that printer is defined in the /etc/cups/printers.conf file. Here is an example of a printer definition in printers.conf:

```
```text
</Printer hp>
<DefaultPrinter printer>
Info Created by redhat-config-printer 0.6.x
DeviceURI parallel:/dev/lp0
Location HP LaserJet 2100M in hall closet
State Idle
Accepting Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
</Printer>
```
```

This is an example of a local printer that serves as the default printer for the local system. The most interesting information relates to the DeviceURI, which shows us that the printer is connected to parallel port /dev/lp0. The State is Idle (ready to accept printer jobs) and the Accepting value is Yes (the printer is accepting print jobs by default).

The Device URI has several ways to identify the device name of a printer, reflecting where the printer is connected. Here are some examples listed in the printers.conf file:

```
```text
DeviceURI parallel:/dev/plp
DeviceURI serial:/dev/ttyd1?baud=38400+size=8+parity=none+flow=soft
DeviceURI scsi:/dev/scsi/scsid610
DeviceURI socket://hostname:port
DeviceURI tftp://hostname/path
DeviceURI ftp://hostname/path
DeviceURI http://hostname[:port]/path
DeviceURI ipp://hostname/path
DeviceURI smb://hostname/printer
```
```

The first three examples show the form for local printers (parallel, serial, and scsi). The other examples are for remote hosts. In each case, hostname can be the host’s name or IP address. Port numbers or paths identify the locations of each printer on the host.