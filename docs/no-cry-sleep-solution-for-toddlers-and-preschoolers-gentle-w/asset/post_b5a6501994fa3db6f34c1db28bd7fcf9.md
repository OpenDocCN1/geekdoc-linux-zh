
## CUPS Directives

Certain directives allow you to place access controls on specific locations. These can be printers or resources, such as the administrative tool or the spool directories. Location controls are implemented with the Location directive. Allow From and Deny From directives can permit or deny access from specific hosts. CUPS supports both Basic and Digest forms of authentication, specified in the AuthType directive. Basic authentication uses a user and password. For example, to use the Web interface, you are prompted to enter the root user and the root user password. Digest authentication makes use of user and password information kept in the CUPS /etc/cups/passwd.md5 file, using MD5 versions of a user and password for authentication. The AuthClass directive specifies the class allowed access. The System class includes the root, sys, and system users. The following example shows the Location directive for the /admin resource, the administrative tool:

```
<Location /admin>

AuthType Basic
AuthClass System

## Restrict access to local domain
Order Deny,Allow
Deny From All
Allow From 127.0.0.1

</Location>
```

## CUPS Command Line Print Clients

Once a print job is placed on a print queue, you can use any of several print clients to manage the printing jobs on your printer or printers, such as Kipp for LPRng and the GNOME Print Manager and the CUPS Printer Configuration Tool for CUPS. You can also use several command line print CUPS clients (for which there are corresponding applications by the same name for LPRng). These include the lpr, lpc, lpq, and lprm commands (see Chapter 10). The Printer System Switcher moves you from one set to the other. With these clients, you can print documents, list a print queue, reorder it, and remove print jobs, effectively canceling them. For network connections, CUPS features an encryption option for its commands, -E, to encrypt print jobs and print information sent over a network. Table 25-2 shows various printer commands.

| Printer Management | Description |
|---|---|
| GNOME Print Manager | GNOME print queue management tool (CUPS). |
| CUPS Configuration Tool | Print, manage, and configure CUPS. |
| lpr options file-list | Prints a file, copies the file to the printer's spool directory, and places it on the print queue to be printed in turn.<br>- P printer prints the file on the specified printer. |
| lpq options | Displays the print jobs in the print queue.<br>- P printer prints the queue for the specified printer.<br>- l prints a detailed listing. |
| lpstat options | Displays printer status. |
| lprm options printjob-id or printer | Removes a print job from the print queue. You identify a particular print job by its number as listed by lpq.<br>- P printer removes all print jobs for the specified printer. |
| lpc | Manages your printers. At the lpc> prompt, you can enter commands to check the status of your printers and take other actions. |

Table 25-2: CUPS Print Clients

### lpr

The lpr client submits a job, and lpd then takes it in turn and places it on the appropriate print queue. lpr takes as its argument the name of a file. If no printer is specified, then the default printer is used. The -P option enables you to specify a particular printer. In the next example, the user first prints the file preface, then prints the file report to the printer with the name myepson:

```
$ lpr preface
$ lpr -P myepson report
```

### lpc

You can use lpc to enable or disable printers, reorder their print queues, and reexecute configuration files. To use lpc, enter the command lpc at the shell prompt. You are then given an lpc> prompt at which you can enter lpc commands to manage your printers and reorder their jobs. The status command with the name of the printer displays whether the printer is ready, how many print jobs it has, and so on. The stop and start commands can stop a printer and start it back up. The printers shown depend on the printers configured for a particular print server. A printer configured on CUPS will only show if you have switched to CUPS. If you switch to the LPRng, those printers you configured for LPRng will show up.

```
# lpc
lpc> status myepson
myepson:
printer is on device 'parallel'
queuing is enabled
printing is enabled
1 entry in spool area
```

### lpq and lpstat

You can manage the print queue using the lpq and lprm commands. The lpq command lists the printing jobs currently on the print queue. With the -P option and the printer name,
