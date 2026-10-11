This parameter controls the behavior of smbd(8) when reporting disk free sizes. By default, this reports a disk block size of 1024 bytes.

Changing this parameter may have some effect on the efficiency of client writes, this is not yet confirmed. This parameter was added to allow advanced administrators to change it (usually to a higher value) and test the effect it has on client write performance without re-compiling the code. As this is an experimental option it may be removed in a future release.

Changing this option does not change the disk free reporting size, just the block size unit reported to the client.

browsable This parameter is a synonym for *browseable*.

browseable (S) Default: *browseable = yes*

This controls whether this share is seen in the list of available shares in a net view and in the browse list.

browse list (G) Default: *browse list = yes*

This controls whether smbd(8) will serve a browse list to a client doing a *Net- ServerEnum* call. Normally set to *yes*. You should never need to change this.

casenames This parameter is a synonym for *case sensitive*.

case sensitive (S) Default: *case sensitive = no*

See the discussion in the section *name mangling*.

change notify timeout (G) Default: *change notify timeout = 60300* *Would change the scan time to every 5 minutes.*

Example: *change notify timeout = 300* *Would change the scan time to every 5 minutes.*

This SMB allows a client to tell a server to "watch" a particular directory for any changes and only reply to the SMB request when a change has occurred. Such constant scanning of a directory is expensive under UNIX, hence an smbd(8) daemon only performs such a scan on each requested directory once every *change notify timeout* seconds.

change share command (G) Default: *No default*

Example: *change share command = /usr/local/bin/addshare*

Samba 2.2.0 introduced the ability to dynamically add and delete shares via the Windows NT 4.0 Server Manager. The *change share command* is used to define an ex-