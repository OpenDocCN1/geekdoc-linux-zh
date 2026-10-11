# msdfs root (S) Default: msdfs root = no

If set to **yes**, Samba treats the share as a Dfs root and allows clients to browse the distributed file system tree rooted at the share directory. Dfs links are specified in the share directory by symbolic links of the form **msdfs:serverA\shareA,serverB\shareB** and so on. For more information on setting up a Dfs tree on Samba, refer to Chapter 19, “Hosting a Microsoft Distributed File System Tree”.

# name cache timeout (G) Default: name cache timeout = 6600

Example: *name cache timeout = 0*

Specifies the number of seconds it takes before entries in samba’s hostname resolve cache time out. If the timeout is set to 0, the caching is disabled.

# name resolve order (G) Default: name resolve order = lmhosts host wins bcast lmhosts

Example: *name resolve order = lmhosts bcast host*

This option is used by the programs in the Samba suite to determine what naming services to use and in what order to resolve host names to IP addresses. Its main purpose is to to control how netbios name resolution is performed. The option takes a space separated string of name resolution options.

The options are: "lmhosts", "host", "wins" and "bcast". They cause names to be resolved as follows:

+   * **lmhosts** : Lookup an IP address in the Samba lmhosts file. If the line in lmhosts has no name type attached to the NetBIOS name (see the [smb.conf(5)](index.html), [lmbosts(5)](index.html) [/usembconfionfof] for details) then any name type matches for lookup.
+   * **host** : Do a standard host name to IP address resolution, using the system /etc/hosts, NIS, or DNS lookups. This method of name resolution is operating system dependent for instance on IRIX or Solaris this may be controlled by the /etc/nsswitch.conf file. Note that this method is used only if the NetBIOS name type being queried is the 0x20 (server) name type or 0x1c (domain controllers). The latter case is only useful for active directory domains and results in a DNS query for the SRV RR entry matching _ldap._tcp.domain.
+   * **wins** : Query a name with the IP address listed in the WINSSERVER parameter. If no WINS server has been specified this method will be ignored.
+   * **bcast** : Do a broadcast on each of the known local interfaces listed in the interfaces parameter. This is the least reliable of the name resolution methods as it depends on the target host being on a locally connected subnet.

The example below will cause the local lmhosts file to be examined first, followed by a broadcast attempt, followed by a normal system hostname lookup.