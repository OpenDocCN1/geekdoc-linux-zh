
is only useful for installations using the Windows NT domain administration tools. The script is free to create a group with an arbitrary name to circumvent unix group name restrictions. In that case the script must print the numeric gid of the created group on stdout.

### add machine script (G) Default: No default

Example: add machine script = /usr/sbin/adduser -n -g machines -c Machine -d /var/lib/nobody -s /bin/false %u

This is the full pathname to a script that will be run by smbd(8) when a machine is added to its domain using the administrator username and password method.

This option is only required when user sam back-ends tied to the Unix uid method of RID calculation such as smbpasswd. This option is only available in Samba 3.0.

### addprinter command (G) Default: No default

Example: addprinter command = /usr/bin/addprinter

With the introduction of MS-RPC based printing support for Windows NT/2000 clients in Samba 2.2, The MS Add Printer Wizard (APW) icon is now also available in the "Printers..." folder displayed a share listing. The APW allows for printers to be add remotely to a Samba or Windows NT/2000 print server.

For a Samba host this means that the printer must be physically added to the underlying printing system. The add printer command defines a script to be run which will perform the necessary operations for adding the printer to the print system and to add the appropriate service definition to the smb.conf file in order that it can be shared by smbd(8).

The addprinter command is automatically invoked with the following parameter (in order):

- printer name
- share name
- port name
- driver name
- location
- Windows 9x driver location

All parameters are filled in from the PRINTER_INFO 2 structure sent by the Windows NT/2000 client with one exception. The "Windows 9x driver location" parameter is included for backwards compatibility only. The remaining fields in the structure are generated from answers to the APW questions.

Once the addprinter command has been executed, smbd will reparse the smb.conf file to determine if the share defined by the APW exists. If the sharename is still invalid, then smbd will return an ACCESS_DENIED error to the client. The "add printer command" program can output a single line of text, which Samba will set as the port the new printer is connected to. If this line isn't output, Samba won't reload its printer shares.

### add share command (G) Default: No default

Example: add_share_command = /usr/local/bin/addshare

Samba 2.2.0 introduced the ability to dynamically add and delete shares via the Windows NT 4.0 Server Manager. The add_share_command is used to define an external program or script which will add a new service definition to smb.conf. In order to successfully execute the add_share_command, smbd requires that the administrator be connected using a root account (i.e. uid == 0).

When executed, smbd will automatically invoke the add_share_command with four parameters.

- configFile - the location of the global smb.conf file.
- shareName - the name of the new share.
- pathName - path to an existing directory on disk.
- comment - comment string to associate with the new share.

This parameter is only used for add file shares. To add printer shares, see the addprinter command.

### add user script (G) Default: No default

Example: add user script = /usr/local/samba/bin/add_user %u

This is the full pathname to a script that will be run AS ROOT by smbd(8) under special circumstances described below.

Normally, a Samba server requires that UNIX users are created for all users accessing files on this server. For sites that use Windows NT account databases as their primary user database creating these users and keeping the user list in sync with the Windows NT PDC is an onerous task. This option allows smbd to create the required UNIX users ON DEMAND when a user accesses the Samba server.

In order to use this option, smbd(8) must NOT be set to security = share and add user script must be set to a full pathname for a script that will create a UNIX user given one argument of %u, which expands into the UNIX user name to create.

When the Windows user attempts to access the Samba server, at login (session setup in the SMB protocol) time, smbd(8) contacts the password server and attempts to authenticate the given user with the given password. If the authentication succeeds then smbd attempts to find a UNIX user in the UNIX password database to map the Windows user into. If this lookup fails, and add user script is set then smbd will call the specified script AS ROOT, expanding any %u argument to be the user name to create.

If this script successfully creates the user then smbd will continue on as though the UNIX user already existed. In this way, UNIX users are dynamically created to match existing Windows NT accounts.

See also security, password server, delete user script.

### add user to group script (G) Default: No default

Example: add user to group script = /usr/sbin/adduser %u %g

Full path to the script that will be called when a user is added to a group using the Windows NT domain administration tools. It will be run by smbd(8) AS ROOT. Any %g will be replaced with the group name and any %u will be replaced with the user name.

Note that the adduser command used in the example below does not support the used syntax on all systems.

### admin users (S) Default: No default

Example: admin users = jason

This is a list of users who will be granted administrative privileges on the share. This means that they will do all file operations as the super-user (root).

You should use this option very carefully, as any user in this list will be able to do anything they like on the share, irrespective of file permissions.

This parameter will not work with the security = share in Samba 3.0. This is by design.

### afs share (S) Default: afs share = no

This parameter controls whether special AFS features are enabled for this Share. If enabled, it assumes that the directory exported via the path parameter is a local AFS import. The special AFS features include the attempt to hand-craft an AFS token if you enabled --with-fake-kaserver in configure.

The mapped user name must contain the cell name to log into, so without setting this parameter there will be no token.

### algorithmic rid base (G) Default: algorithmic rid base = 1000100000

Example: algorithmic rid base = 100000

This determines how Samba will use its algorithmic mapping from uids/gid to the RIDs needed to construct NT Security Identifiers.

Setting this option to a larger value could be useful to sites transitioning from WinNT and Win2k, as existing user and group rids would otherwise clash with system users etc.

All UIDs and GIDs must be able to be resolved into SIDs for the correct operation of ACLs on the server. As such the algorithmic mapping can't be "turned off", but pushing it "out of the way" should resolve the issues. Users and groups can then be assigned "low" RIDs in arbitrary-rid supporting backends.

### allocation roundup size (S) Default: allocation roundup size = 10485760 (to disable roundups)

Example: allocation roundup size = 0 (to disable roundups)

This parameter allows an administrator to tune the allocation size reported to Windows clients. The default size of 1MB generally results in improved Windows client performance. However, rounding the allocation size may cause difficulties for some applications, e.g., MS Visual Studio. If the MS Visual Studio compiler starts to crash with an internal error, set this parameter to zero for this share.

The integer parameter specifies the roundup size in bytes.

### allow trusted domains (G) Default: allow trusted domains = yes

This option only takes effect when the security option is set to server, domain or ads. If it is set to no, then attempts to connect to a resource from a domain or workgroup other than the one which smbd is running in will fail, even if that domain is trusted by the remote server doing the authentication.

This is useful if you only want your Samba server to serve resources to users in the domain it is a member of. As an example, suppose that there are two domains DOMA and DOMB. DOMB is trusted by DOMA, which contains the Samba server. Under normal circumstances, a user with an account in DOMB can then access the resources of a UNIX account with the same account name on the Samba server even if they do not have an account in DOMA. This can make implementing a security boundary difficult.

### announce as (G) Default: announce as = NT Server Win95

Example: announce as = Win95
