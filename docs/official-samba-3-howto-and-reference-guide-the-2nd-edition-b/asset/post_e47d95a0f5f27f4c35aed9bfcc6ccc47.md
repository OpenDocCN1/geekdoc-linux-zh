
You can map Windows usernames that have spaces in them by using double quotes around the name. For example:

```
tridge = "Andrew Tridgell"
```

would map the Windows username "Andrew Tridgell" to the Unix username "tridge".

The following example would map mary and fred to the Unix user sys, and map the rest to guest. Note the use of the '!' to tell Samba to stop processing if it gets a match on that line.

```
!sys = mary fred
guest = *
```

Note that the mapping is applied to all occurrences of usernames. Thus if you connect to \\server\fred and *fred* is remapped to *mary* then you will actually be connecting to \\server\mary and will need to supply a password suitable for *mary* not *fred*. The only exception to this is the username passed to the *password server* (if you have one). The password server will receive whatever username the client supplies without modification.

Also note that no reverse mapping is done. The main effect this has is with printing. Users who have been mapped may have trouble deleting print jobs as PrintManager under WfWg will think they don't own the print job.

Samba versions prior to 3.0.8 would only support reading the fully qualified username (e.g.: DOMAIN\user) from the username map when performing a kerberos login from a client. However, when looking up a map entry for a user authenticated by NTLM\SSP, only the login name would be used for matches. This resulted in inconsistent behavior sometimes even on the same server.

The following functionality is enabled in version 3.0.8 and later:

- When performing local authentication, the username map is applied to the login name before attempting to authenticate the connection.
- When relying upon an external domain controller for validating authentication requests, smbd will apply the username map to the fully qualified username (i.e. DOMAIN\user) only after the user has been successfully authenticated.

An example of use is:

```
username map = /usr/local/samba/lib/users.map
```

*user* This parameter is a synonym for *username*.

*users* This parameter is a synonym for *username*.

### username (S)
**Default:** `username = The guest account if a guest service, else <empty string>`
**Example:** `username = fred, mary, jack, jane, @users, @pcgroup`

Multiple users may be specified in a comma-delimited list, in which case the supplied password will be tested against each username in turn (left to right).

The *username* line is needed only when the PC is unable to supply its own username. This is the case for the COREPLUS protocol or where your users have different WWW usernames to UNIX usernames. In both these cases you may also be better using the \<server\share%user syntax instead.

The *username* line is not a great solution in many cases as it means Samba will try to validate the supplied password against each of the usernames in the *username* line in turn. This is slow and a bad idea for lots of users in case of duplicate passwords. You may get timeouts or security breaches using this parameter unwisely.

Samba relies on the underlying UNIX security. This parameter does not restrict who can login, it just offers hints to the Samba server as to what usernames might correspond to the supplied password. Users can login as whoever they please and they will be able to do no more damage than if they started a telnet session. The daemon runs as the user that they log in as, so they cannot do anything that user cannot do.

To restrict a service to a particular set of users you can use the *valid users* parameter.

If any of the usernames begin in a `'@'` then the name will be looked up first in the NIS netgroups list (if Samba is compiled with netgroup-support), followed by a lookup in the UNIX groups database and will expand to a list of all users in the group of that name.

If any of the usernames begin in a `'+'` then the name will be looked up only in the UNIX groups database and will expand to a list of all users in the group of that name.

If any of the usernames begin in a `'&'` then the name will be looked up only in the NIS netgroups database (if Samba is compiled with netgroup support) and will expand to a list of all users in the netgroup of that name.

Note that searching though a groups database can take quite some time, and some clients may time out during the search.

See the section called "NOTE ABOUT USERNAME/PASSWORD VALIDATION" for more information on how this parameter determines access to the services.

### use sendfile (S)
**Default:** `use sendfile = yes`

If this parameter is *yes*, and the *sendfile(2)* system call is supported by the underlying operating system, then some SMB read calls (mainly *ReadNix* and *ReadRaw*) will use the more efficient *sendfile* system call for files that are exclusively oplocked. This may make more efficient use of the system CPU's and cause Samba to be faster.

Samba automatically turns this off for clients that use protocol levels lower than NT LM 0.12 and when it detects a client is Windows 9x (using sendfile from Linux will cause these clients to fail).

### use spnego (G)
**Default:** `use spnego = yes`

This variable controls whether Samba will try to use Simple and Protected NEGOTIATION (as specified by rfc2195) with Windows XP and Windows 2000 clients to agree upon an authentication mechanism.

Unless further issues are discovered with our SPNEGO implementation, there is no reason this should ever be disabled.

### utmp directory (G)
**Default:** `utmp directory = Determined automatically (/var/run/utmp)`
**Example:** `utmp directory = /var/run/utmp`

This parameter is only available if Samba has been configured and compiled with the option -with-utmp. It specifies a directory pathname that is used to store the utmp or utmpx files (depending on the UNIX system) that record user connections to a Samba server. By default this is not set, meaning the system will use whatever utmp file the native system is set to use (usually */var/run/utmp* on Linux).

### utmp (G)
**Default:** `utmp = no`

This boolean parameter is only available if Samba has been configured and compiled with the option -with-utmp. If set to yes then Samba will attempt to add utmp or utmpx records (depending on the UNIX system) whenever a connection is made to a Samba server. Sites may use this to record the user connecting to a Samba share.

Due to the requirements of the utmp record, we are required to create a unique identifier for the incoming user. Enabling this option creates an N squared algorithm to find this number. This may impede performance on large installations.

### valid users (S)
**Default:** `valid users = No valid users list (anyone can login)`
**Example:** `valid users = grep, @peusers`

This is a list of users that should be allowed to login to this service. Names starting with '@', '+' and '&' are interpreted using the same rules as described in the *invalid users* parameter.

If this is empty (the default) then any user can login. If a username is in both this list and the *invalid users* list then access is denied for that user.

The current servicename is substituted for %S. This is useful in the [homes] section.

### -valid (S)
**Default:** `-valid = yes`

This parameter indicates whether a share is valid and thus can be used. When this parameter is set to false, the share will be in no way visible nor accessible.
This option should not be used by regular users but might be of help to developers.
Samba uses this option internally to mark shares as deleted.

### veto files (S)
**Default:** `veto files = No files or directories are vetoed`

This is a list of files and directories that are neither visible nor accessible. Each entry in the list must be separated by a *`/`*, which allows spaces to be included in the entry. *`*`* and *`?`* can be used to specify multiple files or directories as in DOS wildcards.
Each entry must be a Unix path, not a DOS path and must *not* include the Unix directory separator *`/`*.
Note that the *case sensitive* option is applicable in vetoing files.
One feature of the veto files parameter that it is important to be aware of is Samba's behaviour when trying to delete a directory. If a directory that is to be deleted contains nothing but veto files this deletion will *fail* unless you also set the *delete veto files* parameter to *yes*.
Setting this parameter will affect the performance of Samba, as it will be forced to check all files and directories for a match as they are scanned.
Examples of use include:

```
; Veto any files containing the word Security,
; any ending in .tmp, and any directory containing the
; word root.
veto files = /\*Security\*/\*.tmp/\*root\*/

; Veto the Apple specific files that a NetAtalk server
; creates.
veto files = /.AppleDouble//bin/.AppleDesktop/Network Trash Folder/
```

### veto oplock files (S)
**Default:** `veto oplock files = No files are vetoed for oplock grants`

This parameter is only valid when the *oplocks* parameter is turned on for a share. It allows the Samba administrator to selectively turn off the granting of oplocks on selected files that match a wildcarded list, similar to the wildcarded list used in the *veto files* parameter.
You might want to do this on files that you know will be heavily contended for by clients. A good example of this is the *NetBench* SMB benchmark program, which causes heavy client contention for files ending in *—.SEM—.*. To cause Samba not to grant oplocks on these files you would use the line (either in the *global* section or in the section for the particular NetBench share :
