If a \%p is given then the printer name is put in its place. A \%j is replaced with the job number (an integer).

Note that it is good practice to include the absolute path in the `lprm command` as the `PATH` may not be available to the server.

Examples of use are:

```
```
lprm command = /usr/bin/lprm -P%p %j
or
lprm command = /usr/bin/cancel %p-%j
```
```

# machine password timeout (G)  Default: `machine password timeout = 604800`

If a Samba server is a member of a Windows NT Domain (see the `security = domain` parameter) then periodically a running smbd process will try and change the `MACHINE ACCOUNT PASSWORD` stored in the TDB called `private/secrets.tdb`. This parameter specifies how often this password will be changed, in seconds. The default is one week reexpressed in seconds, the same as a Windows NT Domain member server.

See also smbpasswd(8), and the `security = domain` parameter.

# magic output (S)  Default: `magic output = <magic script name>-outfile.txt`

Example: `magic output = myfile.txt`

This parameter specifies the name of a file which will contain output created by a magic script (see the `magic script` parameter below).

> WARNING
> 
> If two clients use the same *magic script* in the same directory the output file content is undefined.

# magic script (S)  Default: No default

Example: `magic script = user.csh`

This parameter specifies the name of a file which, if opened, will be executed by the server when the file is closed. This allows a UNIX script to be sent to the Samba host and executed on behalf of the connected user.