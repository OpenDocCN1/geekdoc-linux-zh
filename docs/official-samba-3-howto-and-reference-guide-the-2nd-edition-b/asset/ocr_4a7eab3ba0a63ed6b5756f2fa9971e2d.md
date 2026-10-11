Enabling this parameter will disable Samba's support for the SPOOLSS set of MS-RPC's and will yield identical behavior as Samba 2.0.x. Windows NT/2000 clients will downgrade to using LmanSam print spooling commands. Windows 9x/ME will be unaffected by the parameter. However, this will also disable the ability to upload printer drivers to a Samba server via the Windows NT Add Printer Wizard or by using the NT printer properties dialog window. It will also disable the capability of Windows NT/2000 clients to download print drivers from the Samba host upon demand. Be very careful about enabling this parameter.

**display charset (G)** Default: `display charset = ASCIIUTF8`

Example: `display charset = UTF8`

Specifies the charset that samba will use to print messages to stdout and stderr and SWAT will use. Should generally be the same as the *unix charset*.

**dns proxy (G)** Default: `dns proxy = yes`

Specifies that nmbd(8) when acting as a WINS server and finding that a NetBIOS name has not been registered, should treat the NetBIOS name word-for-word as a DNS name and do a lookup with the DNS server for that name on behalf of the name-querying client.

Note that the maximum length for a NetBIOS name is 15 characters, so the DNS name (or DNS alias) can likewise only be 15 characters, maximum.

**nmbd** spawns a second copy of itself to do the DNS name lookup requests, as doing a name lookup is a blocking action.

**domain logons (G)** Default: `domain logons = no`

If set to yes, the Samba server will provide the netlogon service for Windows 9X network logons for the *workgroup* it is in. This will also cause the Samba server to act as a domain controller for NT4 style domain services. For more details on setting up this feature see the Domain Control chapter of the Samba HOWTO Collection.

**domain master (G)** Default: `domain master = auto`

Tell smbd(8) to enable WAN-wide browse list collation. Setting this option causes **nmbd** to claim a special domain specific NetBIOS name that identifies it as a domain master browser for its given *workgroup*. Local master browsers in the same *workgroup* on broadcast-isolated subnets will give this **nmbd** their local browse lists, and then ask **smbd(8)** for a complete copy of the browse list for the whole wide area network. Browser clients will then contact their local master browser, and will receive the domain-wide browse list instead of just the list for their broadcast-isolated subnet.

Note that Windows NT Primary Domain Controllers expect to be able to claim this *workgroup* specific special NetBIOS name that identifies them as domain master browsers for that *workgroup* by default (i.e. there is no way to prevent a Windows