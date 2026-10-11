
The print command is simply a text string. It will be used verbatim after macro substitutions have been made:

- `%s, %f` - the path to the spool file name
- `%p` - the appropriate printer name
- `%J` - the job name as transmitted by the client.
- `%c` - The number of printed pages of the spooled job (if known).
- `%z` - the size of the spooled print job (in bytes)

The print command MUST contain at least one occurrence of `%s` or `%f` - the `%p` is optional. At the time a job is submitted, if no printer name is supplied the `%p` will be silently removed from the printer command.

If specified in the [global] section, the print command given will be used for any printable service that does not have its own print command specified.

If there is neither a specified print command for a printable service nor a global print command, spool files will be created but not processed and (most importantly) not removed.

Note that printing may fail on some UNIXes from the `nobody` account. If this happens then create an alternative guest account that can print and set the *guest account* in the [global] section.

You can form quite complex print commands by realizing that they are just passed to a shell. For example the following will log a print job, print the file, then remove it. Note that `?:` is the usual separator for command in shell scripts.

```
print command = echo Printing %s > /tmp/print.log; lpr -P %p %s; rm %s
```

You may have to vary this command considerably depending on how you normally print files on your system. The default for the parameter varies depending on the setting of the *printing* parameter.

Default: For printing = BSD, AIX, QNX, LPNG or PLP :

```
print command = lpr -r -P%p %s
```

For printing = SYSV or HPUX :

```
print command = lp -c -d%p %s; rm %s
```

For printing = SOFTQ :

```
print command = lp -d%p -s %s; rm %s
```

For printing = CUPS : If SAMBA is compiled against libcups, then *printing* = cups uses the CUPS API to submit jobs, etc. Otherwise it maps to the System V commands with the -oraw option for printing, i.e. it uses `lp -c -d%p -oraw; rm %s`. With *printing* = cups. and if SAMBA is compiled against libcups, any manually set print command will be ignored.

## printer admin (S)
Default: *No default*

Example: *printer admin = admin, @staff*

This lists users who can do anything to printers via the remote administration interfaces offered by MS-RPC (usually using a NT workstation). This parameter can be set per-share or globally. Note: The root user always has admin rights. Use caution with use in the global stanza as this can cause side effects.

## printer
This parameter is a synonym for *printer name*.

## printer name (S)
Default: *printer name = nonlaserwriter*

Example: *printer name = laserwriter*

This parameter specifies the name of the printer to which print jobs spooled through a printable service will be sent.

If specified in the [global] section, the printer name given will be used for any printable service that does not have its own printer name specified.

The default value of the *printer name* may be lp on many systems.

## printing (S)
Default: *No default*

This parameter controls how printer status information is interpreted on your system. It also affects the default values for the *print command*, *lprq command*, *lpqpause command*, *lprsume command* and *lprm command* if specified in the [global] section. Currently nine printing styles are supported. They are BSD, AIX, LPNG, PLP, SYSV, HPUX, QNX, SOFTQ, and CUPS.

To see what the defaults are for the other print commands when using the various options use the testparm(1) program.

This option can be set on a per printer basis. Please be aware however, that you must place any of the various printing commands (e.g. print command, lpq command, etc...) after defining the value for the *printing* option since it will reset the printing commands to default values.

See also the discussion in the section called *The [printers] section*. See also the discussion in the section called *The [printers] section*.

## private dir (G)
Default: *private dir = $(prefix)/private*

This parameter defines the directory smbd will use for storing such files as *smbpasswd* and *secrets.tdb*.

## profile acls (S)
Default: *profile acls = no*

This boolean parameter was added to fix the problems that people have been having with storing user profiles on Samba shares from Windows 2000 or Windows XP clients. New versions of Windows 2000 or Windows XP service packs do security ACL checking on the owner and ability to write of the profile directory stored on a local workstation when copied from a Samba share.

When not in domain mode with winbind then the security info copied onto the local workstation has no meaning to the logged in user (SID) that for workstation so the profile storing fails. Adding this parameter onto a share used for profile storage changes two things about the returned Windows ACL. Firstly it changes the owner and group owner of all reported files and directories to be BUILTIN\\Administrators, BUILTIN\\Users respectively (SIDs S-1-5-32-544, S-1-5-32-545). Secondly it adds an ACE entry of "Full Control" to the SID BUILTIN\\Users to every returned ACL. This will allow any Windows 2000 or XP workstation user to access the profile.

Note that if you have multiple users logging on to a workstation then in order to prevent them from being able to access each others profiles you must remove the "Bypass traverse checking" advanced user right. This will prevent access to other users profile directories as the top level profile directory (named after the user) is created by the workstation profile code and has an ACL restricting entry to the directory tree to the owning user.

## queuepause command (S)
Default: No default

Example: queuepause command = disable %p

This parameter specifies the command to be executed on the server host in order to pause the printer queue.

This command should be a program or script which takes a printer name as its only parameter and stops the printer queue, such that no longer jobs are submitted to the printer.

This command is not supported by Windows for Workgroups, but can be issued from the Printers window under Windows 95 and NT.

If a %p is given then the printer name is put in its place. Otherwise it is placed at the end of the command.

Note that it is good practice to include the absolute path in the command as the PATH may not be available to the server.

## queueresume command (S)
Default: No default

Example: queueresume command = enable %p

This command should be a program or script which takes a printer name as its only parameter and returns the printer name. Such that queued jobs are resubmitted to the printer.

This command is not supported in Windows for Workgroups, but can be issued from the Printers window under Windows 95 and NT.

If a %p is given then the printer name is put in its place. Otherwise it is placed at the end of the command.

Note that it is good practice to include the absolute path in the command as the PATH may not be available to the server.

## read bmpx (G)
Default: read bmpx = no

This boolean parameter controls whether smbd(8) will support the “Read Block Multiple” SMB. This is now rarely used and defaults to no. You should never need to set this parameter.

## read list (S)
Default: No default

Example: *read list = mary, @students*

This is a list of users that are given read-only access to a service. If the connecting user is in this list then they will be given write access, no matter what the read only option is set to. The list can include group names using the syntax described in the *invalid users* parameter.

This parameter will not work with the vfs_fullshare = share in Samba 3.0. This is by design.

## read only (S)
Default: read only = yes

An inverted synonym is *writeable*.

If this parameter is *yes*, then users of a service may not create or modify files in the service's directory.

Note that a printable option (printable = yes) will ALWAYS allow writing to the directory (user profiles etc. etc.), but only via spooling operations.

## read raw (G)
Default: read raw = yes

This parameter controls whether or not the server will support the raw read SMB requests when transferring data to clients.

If enabled, raw reads allow reads of block bytes to one packet. This typically provides a major performance benefit.
