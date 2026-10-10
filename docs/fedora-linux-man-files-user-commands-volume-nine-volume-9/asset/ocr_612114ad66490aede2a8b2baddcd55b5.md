-P|--machine-pass

Use stored machine account password.

-e|--encrypt

This command line parater requires the remote server support the UNIX extensions or that the SMB3 protocol has been selected. Requests that the connection be encrypted. Negotiates SMB encryption using either SMB3 or POSIX extensions via GSSAPI. Uses the given credentials for the encryption negotiation (either kerberos or NTLv1/v2 if given domain/userna/password triple. Fails the connection if encryption cannot be negotiated.

--pw-nt-hash

The supplied password is the NT hash.

-n|--netbiosna <primary NetBIOS na>

This option allows you to override the NetBIOS na that Saa uses for itself. This is identical to setting the **netbios nam**[] parater in the s.conf file. However, a command line setting will take precedence over settings in s.conf.

-i|--scope <scope>

This specifies a NetBIOS scope that nlookup will use to communicate with when generating NetBIOS nas. For details on the use of NetBIOS scopes, see rfc1001.txt and rfc1002.txt. NetBIOS scopes are *very rarely* used, only set this parater if you are the system administrator in charge of all the NetBIOS systems you communicate with.

-W|--workgroup=domain

Set the SMB domain of the userna. This overrides the default domain which is the domain defined in s.conf. If the domain specified is the sa as the servers NetBIOS na, it causes the client to log on using the servers local SAM (as opposed to the Domain SAM).

-O|--socket-options socket options

TCP socket options to set on the client socket. See the socket options parater in the s.conf manual page for the list of valid options.

-?|--help

Print a summary of command line options.

--usage