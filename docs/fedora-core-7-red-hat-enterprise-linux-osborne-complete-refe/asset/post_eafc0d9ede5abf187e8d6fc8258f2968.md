
## Spool Directories

When your system prints a file, it makes use of special directories called *spool directories*. A print job is a file to be printed. When you send a file to a printer, a copy of it is made and placed in a spool directory set up for that printer. The location of the spool directory is obtained from the printer’s entry in its configuration file. In Linux, the spool directory is located at `/var/spool/cups` under a directory with the name of the printer. For example, the spool directory for the `myepson` printer would be located at `/var/spool/cups/myepson`.

The spool directory contains several files for managing print jobs. Some files use the name of the printer as their extension. For example, the `myepson` printer has the files `control.myepson`, which provides printer queue control, and `active.myepson` for the active print job, as well as `log.myepson`, which is the log file.

## Starting the CUPS Server

With the RPM (Remote Print Manager) version used by Red Hat and Fedora, a `cups` startup script is installed in the `/etc/rc.d/init.d` directory. You can start, stop, and restart CUPS using the `service` command and the `cups` script or `system-config-services` (System | Administration | Server Settings | Services). When you make changes or install printers, be sure to restart CUPS to have your changes take effect. You can use the following command:

```bash
# service cups restart
```

## Installing Printers with CUPS

The easiest way to configure and install printers with CUPS is to use `system-config-printer`, as described in Chapter 4, or use the CUPS configuration tool, which is a Web browser–based configuration tool. To ensure browser access, be sure to first select CUPS with the Printer System Switcher, or if you are using `xinetd` for CUPS, turn on cups with the `chkconfig` command.

```bash
# chkconfig cups on
```

To start the Web interface, enter the following URL into your Web browser:

```bash
http://localhost:631
```

This opens an administration screen where you can manage and add printers. You will first be asked to enter the administrator’s username (usually `root`) and password (usually the root user’s password).

With the CUPS configuration tool, you install a printer on CUPS through a series of Web pages, each of which requests different information. To install a printer, click the **Add Printer** button to display a page where you enter the printer name and location. The location is the host to which the printer is connected.

Subsequent pages will prompt you to enter the model of the printer and driver, which you select from available listings. Once you have added the printer, you can configure it. Clicking the **Manage Printers** entry in the Administration page lists your installed printers. You can then click a printer to display a page that lets you control the printer. You can stop the printer, configure its printing, modify its installation, and even delete the printer.

Clicking the **Configure Printer** button displays a page where you can configure how your printer prints, by specifying the resolution or paper size.

Configured information for a printer will be stored in the `/etc/cups/printers.conf` file. You can examine this file directly, and edit it as desired. Here is an example of a printer configuration entry. Notice that it was created using `system-config-printer`. The `DeviceURI` entry specifies the device used, in this case a USB printer managed by HAL. It is currently idle, with no jobs:

```text
# Printer configuration file for CUPS
# Written by cupsd
<Printer mycannon>
    Info Cannon s330
    Location
    DeviceURI hal://org/freedesktop/Hal/devices/usb_device_4a9_1074_300HCR_if0_printer_no_serial
    State Idle
    StateTime 1166554036
    Accepting Yes
    Shared Yes
    JobSheets none none
    QuotaPeriod 0
    PageLimit 0
    KLimit 0
    OpPolicy default
    ErrorPolicy stop-printer
</Printer>
```

> **NOTE** You can perform all administrative tasks from the command line using the `lpadmin` command. See the CUPS documentation for more details.

## Configuring Remote Printers on CUPS

To install a remote printer that is attached to a Windows system or another Linux system running CUPS, you specify its location using special URL protocols. For another CUPS printer on a remote host, the protocol used is `ipp` (Internet Printing Protocol), whereas for a Windows printer, it would be `smb`. Older Unix or Linux systems using LPRng would use the `lpd` protocol.

As shown in Chapter 4, you can use `system-config-printer` to configure a remote printer with CUPS. Create a new printer and select a network type. The entries displayed are different for some network types. A CUPS or LPD remote server will just need the IP address and queue name, whereas the Windows server will need a Samba share name. You can also use the CUPS configuration tool to configure a remote Windows printer. Select the **Windows Printer Via Samba** entry and then enter the appropriate SMB URL.

In the `cupsd.conf` file, for a remote printer, the `DeviceURI` entry, instead of listing the device, will have an Internet address, along with its protocol. For example, a remote printer on a CUPS server (`ipp`) would be indicated as shown here (a Windows printer would use an `smb` protocol):

```text
DeviceURI ipp://mytsuff.com/printers/queue1
```

For a Windows printer, you first need to install, configure, and run Samba. (CUPS uses Samba, which is covered in Chapter 39, to access Windows printers.) When you install the Windows printer on CUPS, you specify its location using the URL protocol `smb`. The user allowed to log in to the printer is entered before the hostname and separated from it by an @ sign. On most configurations, this is the `guest` user. The location entry for a Windows printer called `myhp` attached to a Windows host named `lizard` is shown here. Its Samba share reference would be `//lizard/myhp`:

```text
DeviceURI smb://guest@lizard/myhp
```

To enable CUPS on Samba, you also have to set the printing option in the `/etc/samba/smb.conf` file to `cups`, as shown here:

```text
printing = cups
printcap name = cups
```

To enable CUPS to work with Samba, you have to link the `smbspool` to the CUPS `smb` spool directory:

```bash
ln -s /usr/bin/smbpspool /usr/cups/backend/smb
```

## Configuring a Shared CUPS Printer

To allow a printer to be accessed by the hosts on your local network, you can simply enable printer sharing for that printer. On the host to which the printer is directly connected, use `system-config-printer` to select its printer entry. On the **Settings** panel for that printer, check the **Shared** box under the **State** heading. You can also limit access by users on the **Access** tab. The **Server Settings** tab list an option to share printers on your system.

> **NOTE** To configure a shared Linux printer for access by Windows hosts, you need to configure it as a SMB shared printer. You do this with Samba (see Chapter 39).

## CUPS Printer Classes

CUPS features a way to let you select a group of printers to receive a print job, instead of selecting just one. That way, if one printer is busy or down, another printer can be automatically selected to perform the job. Such groupings of printers are called *classes*. Once you have installed your printers, you can then group them into different classes. For example, you may want to group all inkjet printers into one class and laser printers into another, or you may want to group printers connected to one specific printer server in their own class. To create a class, select **Classes** on the Administration page and enter the name of the class. You can then add printers to it.

## CUPS Configuration

CUPS configuration files are placed in the `/etc/cups` directory. These files are listed in Table 26-2. The `classes.conf`, `printers.conf`, and `client.conf` files can be managed by the Web interface. The `printers.conf` file contains the configuration information for the different printers you have installed. Any of these files can be edited manually, if you wish.

![](img/ab68ea377332b50bf70ef1316c8175b6_590_0.png)
