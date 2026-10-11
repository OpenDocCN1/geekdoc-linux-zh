
## This option tells smbd(8) when acting as a WINS server (wins support = yes) what the maximum ‘time to live’ of NetBIOS names that nmbd will grant will be (in seconds)

This option tells smbd(8) when acting as a WINS server (*wins support = yes*) what the maximum ‘time to live’ of NetBIOS names that **nmbd** will grant will be (in seconds). You should never need to change this parameter. The default is 6 days (518400 seconds).

## max xmit (G)

**Default:** `max xmit = 65535`

**Example:** `max xmit = 8192`

This option controls the maximum packet size that will be negotiated by Samba. The default is 65535, which is the maximum. In some cases you may find you get better performance with a smaller value. A value below 2048 is likely to cause problems.

## message command (G)

**Default:** `No default`

**Example:** `message command = csh -c ‘xedit %s;rm %s’ &`

This specifies what command to run when the server receives a WinPopup style message.

This would normally be a command that would deliver the message somehow. How this is to be done is up to your imagination.

An example is:

```
message command = csh -c ‘xedit %s;rm %s’ &
```

This delivers the message using xedit, then removes it afterwards. *NOTE THAT IT IS VERY IMPORTANT THAT THIS COMMAND RETURN IMMEDIATELY.* That’s why I have the ‘&’ on the end. If it doesn’t return immediately then your PCs may freeze when sending messages (they should recover after 30 seconds, hopefully).

All messages are delivered as the global guest user. The command takes the standard substitutions, although *%u* won’t work (*%U* may be better in this case).

Apart from the standard substitutions, some additional ones apply. In particular:

- *%s* = the filename containing the message.
- *%t* = the destination that the message was sent to (probably the server name).
- *%f* = who the message is from.

You could make this command send mail, or whatever else takes your fancy. Please let us know of any really interesting ideas you have.

Here’s a way of sending the messages as mail to root:

```
message command = /bin/mail -s ‘message from %f on %m’ root < %s; rm %s
```

If you don’t have a message command then the message won’t be delivered and Samba will tell the sender there was an error. Unfortunately *WW* totally ignores the error code and carries on regardless, saying that the message was delivered.

If you want to silently delete it then try:

```
message command = rm %s
```

## min passwd length

This parameter is a synonym for *min password length*.

## min password length (G)

**Default:** `min password length = 5`

This option sets the minimum length in characters of a plaintext password that **smbd** will accept when performing UNIX password changing.

## min print space (S)

**Default:** `min print space = 0`

**Example:** `min print space = 2000`

This sets the minimum amount of free disk space that must be available before a user will be able to spool a print job. It is specified in kilobytes. The default is 0, which means a user can always spool a print job.

## min protocol (G)

**Default:** `min protocol = CORE`

**Example:** `min protocol = NT1`

The value of the parameter (a string) is the lowest SMB protocol dialect that Samba will support. Please refer to the *max protocol* parameter for a list of valid protocol names and a brief description of each. You may also wish to refer to the C source code in *source/smbd/negprot.c* for a listing of known protocol dialects supported by clients.

If you are viewing this parameter as a security measure, you should also refer to the *lanman auth* parameter. Otherwise, you should never need to change this parameter.

## min wins ttl (G)

**Default:** `min wins ttl = 21600`

This option tells **nmbd(8)** when acting as a WINS server (*wins support = yes*) what the minimum 'time to live' of NetBIOS names that **nmbd** will grant will be (in seconds). You should never need to change this parameter. The default is 6 hours (21600 seconds).

## msdfs proxy (S)

**Default:** `No default`

**Example:** `msdfs proxy = \otherserver\someshare`

This parameter indicates that the share is a stand-in for another CIFS share whose location is specified by the value of the parameter. When clients attempt to connect to this share, they are redirected to the proxied share using the SMB-Dfs protocol.

Only *Dfs roots* can act as proxy shares. Take a look at the *msdfs root* and *host msdfs* options to find out how to set up a Dfs root share.

## msdfs root (S)

**Default:** `msdfs root = no`

If set to **yes**, Samba treats the share as a Dfs root and allows clients to browse the distributed file system tree rooted at the share directory. Dfs links are specified in the share directory by symbolic links of the form **msdfs:serverA\shareA,serverB\shareB** and so on. For more information on setting up a Dfs tree on Samba, refer to Chapter 19, “Hosting a Microsoft Distributed File System Tree”.

## name cache timeout (G)

**Default:** `name cache timeout = 6600`

**Example:** `name cache timeout = 0`

Specifies the number of seconds it takes before entries in samba’s hostname resolve cache time out. If the timeout is set to 0, the caching is disabled.

## name resolve order (G)

**Default:** `name resolve order = lmhosts host wins bcast`

**Example:** `name resolve order = lmhosts bcast host`

This option is used by the programs in the Samba suite to determine what naming services to use and in what order to resolve host names to IP addresses. Its main purpose is to control how netbios name resolution is performed. The option takes a space separated string of name resolution options.

The options are: "lmhosts", "host", "wins" and "bcast". They cause names to be resolved as follows:

- **lmhosts**: Lookup an IP address in the Samba lmhosts file. If the line in lmhosts has no name type attached to the NetBIOS name (see the [smb.conf(5)](index.html), [lmhosts(5)](index.html) [smb.conf info](index.html) for details) then any name type matches for lookup.
- **host**: Do a standard host name to IP address resolution, using the system /etc/hosts, NIS, or DNS lookups. This method of name resolution is operating system dependent for instance on IRIX or Solaris this may be controlled by the /etc/nsswitch.conf file. Note that this method is used only if the NetBIOS name type being queried is the 0x20 (server) name type or 0x1c (domain controllers). The latter case is only useful for active directory domains and results in a DNS query for the SRV RR entry matching _ldap._tcp.domain.
- **wins**: Query a name with the IP address listed in the WINSSERVER parameter. If no WINS server has been specified this method will be ignored.
- **bcast**: Do a broadcast on each of the known local interfaces listed in the interfaces parameter. This is the least reliable of the name resolution methods as it depends on the target host being on a locally connected subnet.

The example below will cause the local lmhosts file to be examined first, followed by a broadcast attempt, followed by a normal system hostname lookup.

When Samba is functioning in ADS security mode (security = ads) it is advised to use following settings for name resolve order:

```
name resolve order = wins bcast
```

DC lookups will still be done via DNS, but fallbacks to netbios names will not inundate your DNS servers with needless queries for DOMAIN<0x1c> lookups.

## netbios aliases (G)

**Default:** `netbios aliases = empty string (no additional names)`

**Example:** `netbios aliases = TEST TEST1 TEST2`

This is a list of NetBIOS names that nmbd will advertise as additional names by which the Samba server is known. This allows one machine to appear in browse lists under multiple names. If a machine is acting as a browse server or logon server none of these names will be advertised as either browse server or logon servers, only the primary name of the machine will be advertised with these capabilities.

## netbios name (G)

**Default:** `netbios name = machine DNS name`

**Example:** `netbios name = MYNAME`

This sets the NetBIOS name by which a Samba server is known. By default it is the same as the first component of the host's DNS name. If a machine is a browse server or logon server this name (or the first component of the hosts DNS name) will be the name that these services are advertised under.

## netbios scope (G)

**Default:** `No default`

This sets the NetBIOS scope that Samba will operate under. This should not be set unless every machine on your LAN also sets this value.

## nis homedir (G)

**Default:** `nis homedir = no`
