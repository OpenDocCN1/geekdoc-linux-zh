This command should be a program or script which takes a printer name as its only parameter and outputs printer status information.

Currently nine styles of printer status information are supported: BSD, AIX, LPRNG, PLP, SYSV, HPUX, QNX, CUPS, and SOFTQ. This covers most UNIX systems. You control which type is expected using the `printing` = *option*.

Some clients (notably Windows for Workgroups) may not correctly send the connection number for the printer they are requesting status information about. To get around this, the server reports on the first printer service connected to by the client. This only happens if the connection number sent is invalid.

If a `%p` is given then the printer name is put in its place. Otherwise it is placed at the end of the command.

Note that it is good practice to include the absolute path in the `lpq` *command* as the `$PATH` may not be available to the server. When compiled with the CUPS libraries, no `lpq` *command* is needed because smbd will make a library call to obtain the print queue listing.

# **lpresume command (S)** Default: `lpr` `resume` *command* = `lpr` *command* = `/usr/bin/l-` *pall* `%p-%j` *-p2*

This parameter specifies the command to be executed on the server host in order to restart or continue printing or spooling a specific print job.

This command should be a program or script which takes a printer name and job number to resume the print job. See also the `lppause` *command* parameter.

If a `%p` is given then the printer name is put in its place. A `%j` is replaced with the job number (an integer).

Note that it is good practice to include the absolute path in the `lpr` *resume* *command* as the `PATH` may not be available to the server.

See also the `printing` parameter.

Default: Currently no default value is given to this string, unless the value of the `printing` parameter is SYSV, in which case the default is:

`lp` *-i* `%%p-%%j` *-H* *resume*

or if the value of the `printing` parameter is SOFTQ, then the default is:

`qstat` *-s* *-j* `%%j` *-r*

# **lprm command (S)** Default: `lpr` *m* *command* = *determined by* *printing* *parameter*

This parameter specifies the command to be executed on the server host in order to delete a print job.

This command should be a program or script which takes a printer name and job number, and deletes the print job.