reading calls to check if a file has changed since it was last read. One of these calls uses a one-second granularity; the other uses a two second granularity. As the two second call rounds any odd second down, then if the file has a timestamp of an odd number of seconds then the two timestamps will not match and Visual C++ will keep reporting the file has changed. Setting this option causes the two timestamps to match, and Visual C++ is happy.

**dos filetimes (S)** Default: `dos filetimes = yes`

Under DOS and Windows, if a user can write to a file they can change the timestamp on it. Under POSIX semantics, only the owner of the file or root may change the timestamp. By default, Samba runs with POSIX semantics and refuses to change the timestamp on a file if the user **smbd** is acting on behalf of is not the file owner. Setting this option to `yes` allows DOS semantics and **smbd**(8) will change the file timestamp as DOS requires. Due to changes in Microsoft Office 2000 and beyond, the default for this parameter has been changed from “no” to “yes” in Samba 3.0.14 and above. Microsoft Excel will display dialog box warnings when the file being changed by another user if this parameter is not set to “yes” and files are being shared between users.

**ea support (S)** Default: `ea support = no`

This boolean parameter controls whether **smbd**(8) will allow clients to attempt to store OS/2 style Extended attributes on a share. In order to enable this parameter the underlying filesystem exported by the share must support extended attributes (such as provided on XFS and EXT3 on Linux, with the correct kernel patches). On Linux the filesystem must have been mounted with the mount option user\_xattr in order for extended attributes to work, also extended attributes must be compiled into the Linux kernel.

**enable asu support (G)** Default: `enable asu support = yes`

Hosts running the “Advanced Server for Unix (ASU)” product require some special accommodations such as creating a builtup \[ADMINS\] share that only supports IPC connections. The has been the default behavior in smbd for many years. However, certain Microsoft applications such as the Print Mgrator tool require that the remote server support an \[ADMINS\] file share. Disabling this parameter allows for creating an \[ADMINS\] file share in smb.conf.

**enable privileges (G)** Default: `enable privileges = no`

This parameter controls whether or not **smbd** will honor privileges assigned to specific SIDs via either **net rpc rights** or one of the Windows user and group manager tools. This parameter is disabled by default to prevent members of the Domain Admins group from being able to assign privileges to users or groups which can then result in certain **smbd** operations running as root that would normally run under the context of the connected user.