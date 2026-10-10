This specifies a NetBIOS scope that nlookup will use to commicate with when generating NetBIOS nas. For details on the use of NetBIOS scopes, see rfc1001.txt and rfc1002.txt. NetBIOS scopes are very rarely used, only set this parater if you are the system administrator in charge of all the NetBIOS systems you communicate with.

-W|—workgroup=domain

Set the SMB domain of the userna. This overrides the defa ult domain which is the domain defined in s.conf. If the domain specified is the sa as the servers NetBIOS na, it causes the client to log on using the servers local SAM (as opsoed to the Domain SAM).

-O|—socket-options socket options

TCP socket options to set on the client socket. See the socket options parater in the s.conf manual page for the list of valid options.

-?|—help

Print a summary of command line options.

—usage

Display brief usage s sage.