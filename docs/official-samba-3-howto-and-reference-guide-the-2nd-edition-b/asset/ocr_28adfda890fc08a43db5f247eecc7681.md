The mapped user name must contain the cell name to log into, so without setting this parameter there will be no token.

**algorithmic rid base (G)**  Default: *algorithmic rid base = 1000100000*

*Example:* *algorithmic rid base = 100000*

This determines how Samba will use its algorithmic mapping from uids/gid to the RIDs needed to construct NT Security Identifiers.

Setting this option to a larger value could be useful to sites transitioning from WinNT and Win2k, as existing user and group rids would otherwise clash with syetem users etc.

All UID$s$ and GID$s$ must be able to be resolved into SID$s$ for the correct operation of ACLs on the server. As such the algorithmic mapping can't be \`turned off\` , but pushing it \`out of the way\` should resolve the issues. Users and groups can then be assigned \`low\` RIDs in arbitary-rid supporting backends.

**allocation roundup size (S)**  Default: *allocation roundup size = 10485760* (*to disable roundups*)

*Example:* *allocation roundup size = 0* (*to disable roundups*)

This parameter allows an administrator to tune the allocation size reported to Windows clients. The default size of 1MB generally results in improved Windows client performance. However, rounding the allocation size may cause difficulties for some applications, e.g., MS Visual Studio. If the MS Visual Studio compiler starts to crash with an internal error, set this parameter to zero for this share.

The integer parameter specifies the roundup size in bytes.

**allow trusted domains (G)**  Default: *allow trusted domains = yes*

This option only takes effect when the *security* option is set to *server, domain* or *ads*. If it is set to no, then attempts to connect to a resource from a domain or workgroup other than the one which smbd is running in will fail, even if that domain is trusted by the remote server doing the authentication.

This is useful if you only want your Samba server to serve resources to users in the domain it is a member of. As an example, suppose that there are two domains DOMA and DOMB. DOMB is trusted by DOMA, which contains the Samba server. Under normal circumstances, a user with an account in DOMB can then access the resources of a UNIX account with the same account name on the Samba server even if they do not have an account in DOMA. This can make implementing a security boundary difficult.

**announce as (G)**  Default: *announce as = NT Server* *Win95*

*Example:* *announce as = Win95*