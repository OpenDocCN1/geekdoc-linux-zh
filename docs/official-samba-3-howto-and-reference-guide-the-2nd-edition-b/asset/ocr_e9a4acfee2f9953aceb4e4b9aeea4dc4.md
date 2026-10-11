**-g** This option will list all groups available in the Windows NT domain for which the samba(7) daemon is operating in. Groups in all trusted domains will also be listed. Note that this operation does not assign group ids to any groups that have not already been seen by winbindd(8).

**-get-auth-user** Print username and password used by winbindd during session setup to a domain controller. Username and password can be set using `-A`. Only available for root.

**-G gid** Try to convert a UNIX group id to a Windows NT SID. If the gid specified does not refer to one within the idmap gid range then the operation will fail.

**-I ip** The *-I* option queries winbindd(8) to send a node status request to get the NetBIOS name associated with the IP address specified by the *$p* parameter.

**-im** Produce a list of domains trusted by the Windows NT server winbindd(8) contacts when resolving names. This list does not include the Windows NT domain the server is a Primary Domain Controller for.

**-n name** The *-n* option queries winbindd(8) for the SID associated with the name specified. Domain names can be specified before the user name by using the winbind separator character. For example CWDOM1/Administrator refers to the Administrator user in the domain CWDOM1. If no domain is specified then the domain used is the one specified in the smb.conf(5) *workgroup* parameter.

**-N name** The *-N* option queries winbindd(8) to query the WINS server for the IP address associated with the NetBIOS name specified by the *name* parameter.

**-o user:group** Add a winbind local group as a secondary group for the specified winbindd local user.

**-O user:group** Remove a winbind local group as a secondary group for the specified winbindd local user.

**-p** Check whether winbindd is still alive. Prints out either 'succeeded' or 'failed'.

**-r username** Try to obtain the list of UNIX group ids to which the user belongs. This only works for users defined on a Domain Controller.