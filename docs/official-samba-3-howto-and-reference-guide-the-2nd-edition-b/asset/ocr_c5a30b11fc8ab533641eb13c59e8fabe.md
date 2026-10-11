The second line only works if the printer infotec2105-PS has an already working print queue on the cupsserver and if the printer drivers have been successfully uploaded (via the APW.smbclient /rpcclient, or cupsaddsmb) into the /print$ driver repository of Samba. Some Samba versions prior to version 3.0 required a restart of smbd after the printer install and the driver upload; otherwise the script (or any other client download) would fail. Since there is no easy way to test for the existence of an installed network printer from the logon script, do not bother checking. Just allow the de-installation/re-installation to occur every time a user logs in; it’s really quick anyway (1 to 2 seconds).

The additional benefits for this are:

+   - It puts in place any printer default setup changes automatically at every user logon.
+   - It allows for “roaming” users’ login to the domain from different workstations.

Since network printers are installed per user, this much simplifies the process of keeping the installation up to date. The few extra seconds at logon time will not really be noticeable. Printers can be centrally added, changed, and deleted at will on the server with no user intervention required from the clients (you just need to keep the logon scripts up to date).

# ## 20.11 The addprinter Command

The addprinter command can be configured to be a shell script or program executed by Samba. It is triggered by running the APW from a client against the Samba print server. The APW asks the user to fill in several fields (such as printer name, driver to be used, comment, port monitor, and so on). These parameters are passed on to Samba by the APW. If the addprinter command is designed in a way that it can create a new printer (through writing correct printcap entries on legacy systems or by executing the lpadmin command on more modern systems) and create the associated share, then the APW will in effect really create a new printer on Samba and the UNIX print subsystem!

# ## 20.12 Migration of Classical Printing to Samba

The basic NT-style printer driver management has not changed considerably in 3.0 over the 2.2x releases (apart from many small improvements). Here migration should be quite easy, especially if you followed previous advice to stop using deprecated parameters in your setup. For migrations from an existing 2.0x setup, or if you continued Windows 9x/Me-style printing in your Samba 2.2 installations, it is more of an effort. Please read the appropriate release notes and the HOWTO Collection for Samba-2.2.x. You can follow several paths. Here are possible scenarios for migration:

+   - You need to study and apply the new Windows NT printer and driver support. Previously used parameters printer driver file, printer driver, and printer driver location are no longer supported.
+   - If you want to take advantage of Windows NT printer driver support, you also need to migrate the Windows 9x/Me drivers to the new setup.