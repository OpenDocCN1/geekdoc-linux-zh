
## FIGURE 16.6

Configuring an SMB/CIFS printer requires entering more information than does configuring other types of local or networked printers.

![](img/5d4d3092919d1d16884788127447cc6d_425_0.png)

- User—All Samba print jobs go through one username. You must enter it here. This is the name of a user on the server, not the local machine; the username you enter here need not correspond with a user of the local system.
- Password—You must enter the password for the user authorized to print on the server.

## CAUTION

As the printtool utility warns you, Linux stores the remote system's username and password unencrypted on the local hard disk when you print via an SMB/CIFS queue. This file is called .config and is in the /var/spool/lpd/printername directory. Unfortunately, this file has permissions -rw-r--r--, which means that anybody on the system can read the file. If you restrict the permissions, only root is able to print. This situation therefore represents a potentially major security problem for the print server. You can reduce the severity of the problem by creating a special print-only account on the server. If the server uses share-level security, of course, the username is irrelevant and the password only accesses the printer share, assuming that the server is configured with different passwords for all services.

- Workgroup—The name of the domain or workgroup on which the server resides.

When you finish defining the printer queue, you can print to it much as you would to any Linux printer queue. You can use the lp command to print a document, as in lp fly.ps; or you can print by using the print commands in the applications you use. There isn't any indication that the printer queue is a Samba queue, just that it exists along with any other local or remote printer queues you might have defined on your system (assuming that the application lists the available queues; not all do).

## Configuring a Queue Manually

If you're not using Red Hat Linux, you should consult your distribution's documentation for information on configuring a Samba printer queue. If your documentation lacks this information, follow these steps:

1. Create a printer in whatever way you normally would.
2. Change the lp= entry in /etc/printcap to point to /dev/null.
3. Create a file called .config in the spool directory for your printer (/var/spool/lpd/printername), and type these lines in that file:
   server=servername
   service=printername
   password=password

You should replace servername, printername, and password with appropriate strings, of course.

## Note

> The standard smbprint script file passes the server's name as the username. This is unimportant if the server is set for share-level security, but if the server is set for user-level security, the server must have an account named after itself with the password specified in the .config file. Alternatively, you could alter the smbprint script on the Linux client.

4. Change the if= line in /etc/printcap to point to the smbprint script. This script might be in /usr/bin, /usr/local/bin, or elsewhere, depending on your distribution.
5. Change the af= line in /etc/printcap, or add one if necessary, to create an accounting file. This can be a file in the spool directory. Its name is unimportant, so long as it doesn't overwrite an existing file. For instance af=/var/spool/lpd/printername/afile should do fine.
6. Restart the printer queue.

The new queue should now work, with one major caveat: Step 4 replaces your filter file, and if you had configured your printer queue to use a smart filter to process PostScript into something that the printer understands, you've now lost that ability. You might therefore want to create a new script that both calls the old print filter and calls smbprint. You can then enter this new script as the new filter file for the queue. If the server is a Linux computer with its own Ghostscript queues, of course you can print PostScript to the remote system and the remote system will do the Ghostscript processing. PostScript processing also happens remotely
