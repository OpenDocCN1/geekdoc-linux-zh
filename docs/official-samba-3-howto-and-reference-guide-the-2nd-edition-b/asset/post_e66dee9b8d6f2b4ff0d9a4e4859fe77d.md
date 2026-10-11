
An example of how privileges can be used is to assign the right to join clients to a Samba controlled domain without providing root access to the server via smbd.

Please read the extended description provided in the Samba documentation before enabling this option.

## enable rid algorithm (G)

Default: `enable rid algorithm = yes`

This option is used to control whether or not smbd in Samba 3.0 should fallback to the algorithm used by Samba 2.2 to generate user and group RIDs. The long-term development goal is to remove the algorithmic mappings of RIDs altogether, but this has proved to be difficult. This parameter is mainly provided so that developers can turn the algorithm on and off and see what breaks. This parameter should not be disabled by non-developers because certain features in Samba will fail to work without it.

## encrypt passwords (G)

Default: `encrypt passwords = yes`

This boolean controls whether encrypted passwords will be negotiated with the client. Note that Windows NT 4.0 SP3 and above and also Windows 98 will by default expect encrypted passwords unless a registry entry is changed. To use encrypted passwords in Samba see the chapter "User Database" in the Samba HOWTO Collection.

MS Windows clients that expect Microsoft encrypted passwords and that do not have plain text password support enabled will be able to connect only to a Samba server that has encrypted password support enabled and for which the user accounts have a valid encrypted password. Refer to the *smbpasswd* command man page for information regarding the creation of encrypted passwords for user accounts.

The use of plain text passwords is NOT advised as support for this feature is no longer maintained in Microsoft Windows products. If you want to use plain text passwords you must set this parameter to `no`.

In order for encrypted passwords to work correctly smbd(8) must either have access to a local *smbpasswd(5)* file (see the *smbpasswd(8)* program for information on how to set up and maintain this file), or set the `security = [server|domain|ads]` parameter which causes smbd to authenticate against another server.

## enhanced browsing (G)

Default: `enhanced browsing = yes`

This option enables a couple of enhancements to cross-subnet browse propagation that have been added in Samba but which are not standard in Microsoft implementations.

The first enhancement to browse propagation consists of a regular wildcard query to a Samba WINS server for all Domain Master Browsers, followed by a browse synchronization with each of the returned DMBs. The second enhancement consists of a regular randomised browse synchronization with all currently known DMBs.

These enhancements can cause an empty workgroup to stay around forever which can be annoying.

In general you should leave this option enabled as it makes cross-subnet browse propagation much more reliable.

## enumports command (G)

Default: No default

Example: `enumports command = /usr/bin/listports`

The concept of a "port" is fairly foreign to UNIX hosts. Under Windows NT/2000 print servers, a port is associated with a port monitor and generally takes the form of a local port (i.e. LPT1:, COM1:, FILE:) or a remote port (i.e. LPD Port Monitor, etc...). By default, Samba has only one port defined - "Samba Printer Port". Under Windows NT/2000, all printers must have a valid port name. If you wish to have a list of ports displayed (**smbd** does not use a port name for anything) other than the default "Samba Printer Port", you can define **enumports command** to point to a program which should generate a list of ports, one per line, to *standard output*. This listing will then be used in response to the level 1 and 2 EnumPorts() RPC.

## fake directory create times (S)

Default: `fake directory create times = no`

NTFS and Windows VFAT file systems keep a create time for all files and directories. This is not the same as the ctime - status change time - that Unix keeps, so Samba by default reports the earliest of the various times Unix does keep. Setting this parameter for a share causes Samba to always report midnight 1-1-1980 as the create time for directories.

This option is mainly used as a compatibility option for Visual C++ when used against Samba shares. Visual C++ generated makefiles have the object directory as a dependency for each object file, and a make rule to create the directory. Also, when NMAKE compares timestamps it uses the create time when examining a directory. Thus the object directory will be created if it does not exist, but once it does exist it will always have an earlier timestamp than the object files it contains.

However, Unix time semantics mean that the create time reported by Samba will be updated whenever a file is created or deleted in the directory. NMAKE finds all object files in the object directory. The timestamp of the last one built is then compared to the timestamp of the object directory. If the directory's timestamp is newer, then all object files will be rebuilt. Enabling this option ensures directories always predate their contents and an NMAKE build will proceed as expected.

## fake oplocks (S)

Default: `fake oplocks = no`

Oplocks are the way that SMB clients get permission from a server to locally cache file operations. If a server grants an oplock (opportunistic lock) then the client is free to assume that it is the only one accessing the file and will aggressively cache file data. With some oplock types the client may even cache file open/close operations. This can give enormous performance benefits.

When you set `fake oplocks = yes`, smbd(8) will always grant oplock requests no matter how many clients are using the file.

> It is generally much better to use the real *oplocks* support rather than this parameter.
>
> If you enable this option on all read-only shares or shares that you know will only be accessed from one *client* at a time such as physically read-only media like CDROMs, you will see a big performance improvement on many operations. If you enable this option on shares where multiple clients may be accessing the files read-write at the same time you can get data corruption. Use this option carefully!

## follow symlinks (S)

Default: `follow symlinks = yes`

This parameter allows the Samba administrator to stop smbd(8) from following symbolic links in a particular share. Setting this parameter to `no` prevents any file or directory that is a symbolic link from being followed (the user will get an error). This option is very useful to stop users from adding a symbolic link to */etc/passwd* in their home directory for instance. However it will slow filename lookups down slightly.

This option is enabled (i.e. **smbd** will follow symbolic links) by default.

## force create mode (S)

Default: `force create mode = 0000755`

Example: `force create mode = 0755`

This parameter specifies a set of UNIX mode bit permissions that will *always* be set on a file created by Samba. This is done by bitwise 'OR'ing these bits onto the mode bits of a file that is being created or having its permissions changed. The default for this parameter is (in octal) 000. The modes in this parameter are bitwise 'OR'ed onto the file mode after the mask set in the *create mask* parameter is applied.

The example below would force all created files to have read and execute permissions set for 'group' and 'other' as well as the read/write/execute bits set for the 'user'.

## force directory mode (S)

Default: `force directory mode = 0000755`

Example: `force directory mode = 0755`

This parameter specifies a set of UNIX mode bit permissions that will *always* be set on a directory created by Samba. This is done by bitwise 'OR'ing these bits onto the mode bits of a directory that is being created. The default for this parameter is (in octal) 0000 which will not add any extra permission bits to a created directory. This operation is done after the mode mask in the parameter *directory mask* is applied.

The example below would force all created directories to have read and execute permissions set for 'group' and 'other' as well as the read/write/execute bits set for the 'user'.

## force directory security mode (S)

Default: `force directory security mode = 0700`
