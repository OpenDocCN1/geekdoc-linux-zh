
This command should be a program or script which takes a printer name as its only parameter and outputs printer status information.

Currently nine styles of printer status information are supported: BSD, AIX, LPRNG, PLP, SYSV, HPUX, QNX, CUPS, and SOFTQ. This covers most UNIX systems. You control which type is expected using the `printing` = *option*.

Some clients (notably Windows for Workgroups) may not correctly send the connection number for the printer they are requesting status information about. To get around this, the server reports on the first printer service connected to by the client. This only happens if the connection number sent is invalid.

If a `%p` is given then the printer name is put in its place. Otherwise it is placed at the end of the command.

Note that it is good practice to include the absolute path in the `lpq` *command* as the `$PATH` may not be available to the server. When compiled with the CUPS libraries, no `lpq` *command* is needed because smbd will make a library call to obtain the print queue listing.

## lpr resume command (S)
Default: `lpr` `resume` *command* = `lpr` *command* = `/usr/bin/lpq` `%p`

This parameter specifies the command to be executed on the server host in order to restart or continue printing or spooling a specific print job.

This command should be a program or script which takes a printer name and job number to resume the print job. See also the `lppause` *command* parameter.

If a `%p` is given then the printer name is put in its place. A `%j` is replaced with the job number (an integer).

Note that it is good practice to include the absolute path in the `lpr` *resume* *command* as the `PATH` may not be available to the server.

See also the `printing` parameter.

Default: Currently no default value is given to this string, unless the value of the `printing` parameter is SYSV, in which case the default is:

`lp` *-i* `%%p-%%j` *-H* *resume*

or if the value of the `printing` parameter is SOFTQ, then the default is:

`qstat` *-s* *-j* `%%j` *-r*

## lprm command (S)
Default: `lpr` *m* *command* = *determined by* *printing* *parameter*

This parameter specifies the command to be executed on the server host in order to delete a print job.

This command should be a program or script which takes a printer name and job number, and deletes the print job.

If a `%p` is given then the printer name is put in its place. A `%j` is replaced with the job number (an integer).

Note that it is good practice to include the absolute path in the `lprm` *command* as the `PATH` may not be available to the server.

Examples of use are:

```text
lprm command = /usr/bin/lprm -P%p %j
or
lprm command = /usr/bin/cancel %p-%j
```

## machine password timeout (G)
Default: `machine password timeout = 604800`

If a Samba server is a member of a Windows NT Domain (see the `security = domain` parameter) then periodically a running smbd process will try and change the `MACHINE ACCOUNT PASSWORD` stored in the TDB called `private/secrets.tdb`. This parameter specifies how often this password will be changed, in seconds. The default is one week reexpressed in seconds, the same as a Windows NT Domain member server.

See also smbpasswd(8), and the `security = domain` parameter.

## magic output (S)
Default: `magic output = <magic script name>-outfile.txt`

Example: `magic output = myfile.txt`

This parameter specifies the name of a file which will contain output created by a magic script (see the `magic script` parameter below).

> **WARNING**
>
> If two clients use the same *magic script* in the same directory the output file content is undefined.

## magic script (S)
Default: No default

Example: `magic script = user.csh`

This parameter specifies the name of a file which, if opened, will be executed by the server when the file is closed. This allows a UNIX script to be sent to the Samba host and executed on behalf of the connected user.

Scripts executed in this way can be deleted upon completion assuming that the user has the appropriate level of privilege and the file permissions allow the deletion.

If the script generates output, output will be sent to the file specified by the *magic output* parameter (see above).

Note that some shells are unable to interpret scripts containing CR/LF instead of LF as the end-of-line marker. Magic scripts must be executable *as* is on the host, which for some hosts and some shells will require filtering at the DOS end.

Magic scripts are *EXPERIMENTAL* and should *NOT* be relied upon.

## mangled map (S)
Default: *mangled map = no*

Example: *mangled map = (*.html *.htm)*

This is for those who want to directly map UNIX file names which cannot be represented on Windows/DOS. The mangling of names is not always what is needed. In particular you may have documents with file extensions that differ between DOS and UNIX. For example, under UNIX it is common to use *.html* for HTML files, whereas under Windows/DOS *.htm* is more commonly used.

So to map *html* to *htm* you would use:

```text
mangled map = (*.html *.htm)
```

One very useful case is to remove the annoying *;1* off the ends of filenames on some CDROMs (only visible under some UNIXes). To do this use a map of `(;;1;)`.

## mangled names (S)
Default: *mangled names = yes*

This controls whether non-DOS names under UNIX should be mapped to DOS-compatible names (“mangled”) and made visible, or whether non-DOS names should simply be ignored.

See the section on *name mangling* for details on how to control the mangling process.

If mangling is used then the mangling algorithm is as follows:

- The first (up to) five alphanumeric characters before the rightmost dot of the filename are preserved, forced to upper case, and appear as the first (up to) five characters of the mangled name.
- A tilde `~` is appended to the first part of the mangled name, followed by a two-character unique sequence, based on the original root name (i.e., the original filename minus its final extension). The final extension is included in the hash calculation only if it contains any upper case characters or is longer than three characters.
- Files whose UNIX name begins with a dot will be presented as DOS hidden files. The mangled name will be created as for other filenames, but with the leading dot removed and `___` as its extension regardless of actual original extension (that's three underscores).

Note that the character to use may be specified using the *mangling char* option, if you don’t like `~`.

The two-digit hash value consists of upper case alphanumeric characters.

This algorithm can cause name collisions only if files in a directory share the same first five alphanumeric characters. The probability of such a clash is 1/1300.

The name mangling (if enabled) allows a file to be copied between UNIX directories from Windows/DOS while retaining the long UNIX filename. UNIX files can be renamed to a new extension from Windows/DOS and will retain the same basename. Mangled names do not change between sessions.

## mangle prefix (G)
Default: mangle prefix = 14

Example: mangle prefix = 4

controls the number of prefix characters from the original name used when generating the mangled names. A larger value will give a weaker hash and therefore more name collisions. The minimum value is 1 and the maximum value is 6.

mangle prefix is effective only when mangling method is hash2.

## mangling char (S)
Default: mangling char = `~`

Example: mangling char = `^`

This controls what character is used as the magic character in name mangling. The default is a `~` but this may interfere with some software. Use this option to set it to whatever you prefer. This is effective only when mangling method is hash.

## mangling method (G)
Default: mangling method = hash2

Example: mangling method = hash

controls the algorithm used for the generating the mangled names. Can take two different values, "hash" and "hash2". "hash" is the algorithm that was used in Samba for many years and was the default in Samba 2.2.x. "hash2" is now the default and is newer and considered a better algorithm (generates less collisions) in the names. Many Win32 applications store the mangled names and so changing to algorithm must not be done lightly as these applications may break unless reinstalled.

## map acl inherit (S)
Default: map acl inherit = no

This boolean parameter controls whether smbd(8) will attempt to map the 'inherit' and 'protected' access control entry flags stored in Windows ACLs into an extended attribute called user.SAMBA:PAI. This parameter only takes effect if Samba is being run on a platform that supports extended attributes (Linux and IRIX so far) and
