# 704 Part V Running Servers

The DeviceURI is lined with the key information. It identifies the location (an sm object), username (jjones), user's password (my9passwd), workgroup (FSTREET), server (NS1), and printer queue name (hp).

The contents of the cupsd.conf file define who you allow to use this printer.

```
<Location /printers/NS1-PS>
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
AuthType None
</Location>
```

Based on this example information, only users from the local host (127.0.0.1) are allowed to use the printer, and no authentication is necessary for them to use it.

If everything is set up properly, you can use the standard lpr command to print the file to the printer. Using this example, employ the following form for printing:

```
$ file1.ps | lpr -P NS1-PS
```

> If you are receiving failure messages, make sure that the computer to which you are printing is accessible. For the Printer NS1-PS example, use type smclient-L NS1 -U jones. Then type the password (mypasswd, in this case). If you get a positive query response after you enter a password, you should see a list of shared printers and files from that server. Check the names, and try printing again.

# Adding a NetPrinter

To set up your Linux system by a printer that is connected to (or otherwise managed by) NetWare file and print server, you must gather the information about the server, user, and password.

Select to add a Novell printer (Novell created NetWare) to the Printer Configuration window (described previously), and then fill in the following information:

+   * Server — Name of the computer to which the printer is attached (or otherwise accessible). This is the NetWare server name for the computer.
* Queue — Name of the print queue on the NetWare server.
* User — Username required by the NetWare system to enable access to the NetWare printer.
* Password — Password associated with the username.

Complete the rest of the procedure as a local printer (see the “Adding a Local Printer in Red Hat” section earlier in this chapter).