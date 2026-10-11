# **printer admin (S)** Default: *No default*

Example: *printer admin = admin, @staff*

This lists users who can do anything to printers via the remote administration interfaces offered by MS-RPC (usually using a NT workstation). This parameter can be set per-share or globally. Note: The root user always has admin rights. Use caution with use in the global stanza as this can cause side effects.

# **printer** This parameter is a synonym for *printer name*.

# **printer name (S)** Default: *printer name = nonlaserwriter*

Example: *printer name = laserwriter*

This parameter specifies the name of the printer to which print jobs spooled through a printable service will be sent.

If specified in the [global] section, the printer name given will be used for any printable service that does not have its own printer name specified.

The default value of the *printer name* may be lp on many systems.

# **printing (S)** Default: *No default*

This parameters controls how printer status information is interpreted on your system. It also affects the default values for the *print command*, *lprq command*, *lpqpause command*, *lprsume command* and *lprm command* if specified in the [global] section. Currently nine printing styles are supported. They are BSD, AIX, LPNG, PLP, SYSV, HPUX, QNX, SOFTQ, and CUPS.

To see what the defaults are for the other print commands when using the various options use the testparm(1) program.

This option can be set on a per printer basis. Please be aware however, that you must place any of the various printing commands (e.g. print command, lpq command, etc...) after defining the value for the *printing* option since it will reset the printing commands to default values.

See also the discussion in the the section called \$\ref{The [printers] section\ref{ section. See also the discussion in the the section called \$\ref{The [printers] section\ref{

# **private dir (G)** Default: *private dir = $(prefix)/private*

This parameters defines the directory smbd will use for storing such files as *smbpasswd* and *secrets.tdb*.

# **profile acls (S)** Default: *profile acls = no*