
## 20.9.4 The Installation Client

More information regarding the Imprints installation client is available from the documentation file Imprints-Client-HOWTO.ps that is included with the Imprints source package. The Imprints installation client comes in two forms:

- A set of command-line Perl scripts.
- A GTK+-based graphical interface to the command-line Perl scripts.

The installation client (in both forms) provides a means of querying the Imprints database server for a matching list of known printer model names as well as a means to download and install the drivers on remote Samba and Windows NT print servers.

The basic installation process is in four steps, and Perl code is wrapped around smbclient and rpcclient.

- For each supported architecture for a given driver:
    - 1. rpcclient: Get the appropriate upload directory on the remote server.
    - 2. smbclient: Upload the driver files.
    - 3. rpcclient: Issues an AddPrinterDriver() MS-RPC.
- rpcclient: Issues an AddPrinterEx() MS-RPC to actually create the printer.

One of the problems encountered when implementing the Imprints tool set was the namespace issues between various supported client architectures. For example, Windows NT includes a driver named “Apple LaserWriter II NTX v51.8”. And Windows 95 calls its version of this driver “Apple LaserWriter II NTX”.

The problem is how to know what client drivers have been uploaded for a printer. An astute reader will remember that the Windows NT Printer Properties dialog only includes space for one printer driver name. A quick look in the Windows NT 4.0 system registry at:
`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Print\Environment`
will reveal that Windows NT always uses the NT driver name. This is okay because Windows NT always requires that at least the Windows NT version of the printer driver is present. Samba does not have the requirement internally; therefore, “How can you use the NT driver name if it has not already been installed??”

The way of sidestepping this limitation is to require that all Imprints printer driver packages include both the Intel Windows NT and 95/98 printer drivers and that the NT driver is installed first.

## 20.10 Adding Network Printers without User Interaction

The following MS Knowledge Base article may be of some help if you need to handle Windows 2000 clients: How to Add Printers with No User Interaction in Windows 2000, (Microsoft KB 189105^5). It also applies to Windows XP Professional clients. The ideas sketched out in this section are inspired by this article, which describes a command-line method that can be applied to install network and local printers and their drivers. This is most useful if integrated in Logon Scripts. You can see what options are available by typing in the command prompt (DOS box):

```
rundll32 printui.dll,PrintUIEntry /?
```

A window pops up that shows you all of the command-line switches available. An extensive list of examples is also provided. This is only for Windows 200x/XP; it does not work on Windows NT. Windows NT probably has some other tools in the respective Resource Kit. Here is a suggestion about what a client logon script might contain, with a short explanation of what the lines actually do (it works if 200x/XP Windows clients access printers via Samba, and works for Windows-based print servers too):

```
rundll32 printui.dll,PrintUIEntry /dn /n "\\cupserver\\infotec2105-IPDS" /q
rundll32 printui.dll,PrintUIEntry /in /n "\\cupserver\\infotec2105-PS"
rundll32 printui.dll,PrintUIEntry /y /n "\\cupserver\\infotec2105-PS"
```

Here is a list of the used command-line parameters:

- /dn deletes a network printer.
- /q quiet mode.
- /n names a printer.
- /in adds a network printer connection.
- /y sets printer as default printer.

- Line 1 deletes a possibly existing previous network printer *infotec2105-IPDS* (which had used native Windows drivers with LPRng that were removed from the server that was converted to CUPS). The /q at the end prevents confirm or error dialog boxes from popping up. They should not be presented to the user logging on.
- Line 2 adds the new printer *infotec2105-PS* (which actually is the same physical device but is now run by the new CUPS printing system and associated with the CUPS/Adobe PS drivers). The printer and its driver must have been added to Samba prior to the user logging in (e.g., by a procedure as discussed earlier in this chapter or by running **cupsaddsmb**). The driver is now auto-downloaded to the client PC where the user is about to log in.
- Line 3 sets the default printer to this new network printer (there might be several other printers installed with this same method, and some may be local as well, so we decide for a default printer). The default printer selection may, of course, be different for different users.

The second line only works if the printer infotec2105-PS has an already working print queue on the cups server and if the printer drivers have been successfully uploaded (via the APW smbclient /rpcclient, or cupsaddsmb) into the /print$ driver repository of Samba. Some Samba versions prior to version 3.0 required a restart of smbd after the printer install and the driver upload; otherwise the script (or any other client download) would fail. Since there is no easy way to test for the existence of an installed network printer from the logon script, do not bother checking. Just allow the de-installation/re-installation to occur every time a user logs in; it’s really quick anyway (1 to 2 seconds).

The additional benefits for this are:

- It puts in place any printer default setup changes automatically at every user logon.
- It allows for “roaming” users’ login to the domain from different workstations.

Since network printers are installed per user, this much simplifies the process of keeping the installation up to date. The few extra seconds at logon time will not really be noticeable. Printers can be centrally added, changed, and deleted at will on the server with no user intervention required from the clients (you just need to keep the logon scripts up to date).

### 20.11 The addprinter Command

The addprinter command can be configured to be a shell script or program executed by Samba. It is triggered by running the APW from a client against the Samba print server. The APW asks the user to fill in several fields (such as printer name, driver to be used, comment, port monitor, and so on). These parameters are passed on to Samba by the APW. If the addprinter command is designed in a way that it can create a new printer (through writing correct printcap entries on legacy systems or by executing the lpadmin command on more modern systems) and create the associated share, then the APW will in effect really create a new printer on Samba and the UNIX print subsystem!

### 20.12 Migration of Classical Printing to Samba

The basic NT-style printer driver management has not changed considerably in 3.0 over the 2.2x releases (apart from many small improvements). Here migration should be quite easy, especially if you followed previous advice to stop using deprecated parameters in your setup. For migrations from an existing 2.0x setup, or if you continued Windows 9x/Me-style printing in your Samba 2.2 installations, it is more of an effort. Please read the appropriate release notes and the HOWTO Collection for Samba-2.2.x. You can follow several paths. Here are possible scenarios for migration:

- You need to study and apply the new Windows NT printer and driver support. Previously used parameters printer driver file, printer driver, and printer driver location are no longer supported.
- If you want to take advantage of Windows NT printer driver support, you also need to migrate the Windows 9x/Me drivers to the new setup.
- An existing printers.def file (the one specified in the now removed parameter printer driver file) will no longer work with Samba-3. In 3.0, smbd attempts to locate Windows 9x/Me driver files for the printer in [print$] and additional settings in the TDB and only there; if it fails, it will not (as 2.2.x) drop down to using a printers.def (and all associated parameters). The make_printerdef tool is removed and there is no backward compatibility for this.
- You need to install a Windows 9x/Me driver into the [print$] share for a printer on your Samba host. The driver files will be stored in the *WIN40/0* subdirectory of [print$], and some other settings and information go into the printing-related TDBs.
- If you want to migrate an existing printers.def file into the new setup, the only current solution is to use the Windows NT APW to install the NT drivers and the 9x/Me drivers. This can be scripted using smbclient and rpcclient. See the Imprints installation client on the Imprints® web site for example. See also the discussion of rpcclient usage in Chapter 21, *CUPS Printing Support*.

## 20.13 Publishing Printer Information in Active Directory or LDAP

This topic has also been addressed in Chapter 12, *Remote and Local Management: The Net Command*. If you wish to volunteer your services to help document this further, please contact John H. Terpstra⁹.

## 20.14 Common Errors

### 20.14.1 I Give My Root Password but I Do Not Get Access

Do not confuse the root password, which is valid for the UNIX system (and in most cases stored in the form of a one-way hash in a file named /etc/shadow), with the password used to authenticate against Samba. Samba does not know the UNIX password. Root access to Samba resources requires that a Samba account for root must first be created. This is done with the smbpasswd command as follows:

```
root# smbpasswd -a root
New SMB password: secret
Retype new SMB password: secret
```

### 20.14.2 My Print Jobs Get Spooled into the Spooling Directory, but Then Get Lost

Do not use the existing UNIX print system spool directory for the Samba spool directory. It may seem convenient and a savings of space, but it only leads to problems. The two
