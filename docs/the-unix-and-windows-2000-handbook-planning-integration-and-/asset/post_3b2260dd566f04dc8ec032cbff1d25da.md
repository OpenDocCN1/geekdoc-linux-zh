
search_path =       /etc
browsable_dirs =    yes
show_statfs_entries = no
fully_qualified_hosts = no
cache_duration =    300

# DEFINE AN AMD MOUNT POINT
[ /home ]
map_name =          amd.home
[ /tools ]
map_name =          amd.mf
[ /net ]
map_name =          amd.net

The right-hand side of the equal sign (=) in the regular map section contains the name of the mount map. and supports regular files, NDBM databases, NIS maps, NIS+ maps, LDAP maps, and a few other mount map forms. The map_type parameter in the global section of the example above specifies the use of NIS maps. A portion of the text file that will become the NIS mount map, amd.mf, is provided in the next example. To access the information in these directories, a user would only need to cd to /tools/solcad and /tools/cadence434. The actual mount points would be /a/yamacraw.company.com/export/home1/solaris/ic and /a/yamacraw.company.com/export/home1/cadence434 for machines other than yamacraw. The mount points for users on the yamacraw machine would be /export/home1/solaris/ic and /export/home1/cadence434.

This is just a simple example of the syntax for creating amd maps. This file requires further processing before it can become an NIS map. There are more than 20 selector variables that allow you to "tailor" your mount points for things such as machine architecture, operating system, or operating system version. You can also specify options used by the mount command for each map. The default option for each map is "rw.defaults". As you can see, And provides a lot of flexibility and features for mount maps that are not available in the automounter package.

```
solcad
hostd!=yamacraw.company.com;
    type:=nfs;
    rfs:=/export/home1/solaris;
    sublink:=ic;
    rhost:=yamacraw.company.com
hostd==yamacraw.company.com;
    type:=link;
    fs:=/export/home1/solaris;
    sublink:=ic;
```

```
#
cadence434
hostd!=yamacraw.company.com:
type:=nfs;
rfs:=/export/home1;
sublink:=cadence434;
rhost:=yamacraw.company.com
hostd==yamacraw.company.com
type:=link;
fs:=/export/home1;
sublink:=cadence434;
#
```

Monitoring the state of amd is accomplished with the amq command, which is RPC-based. The default output is a list of mount points and automounted filesystems on the current system. Table 8.5 contains a listing of the more frequently used options for amq. The following contains an example of the amq command with the -m option.

```
"root" youdee:(pid157) root 1 localhost is up
amd.home /home toplvl 1 localhost is up
amd.mf /tools toplvl 1 localhost is up
amd.net /net toplvl 1 localhost is up
duchess:/export/home1 /a/duchess/export/home1 nfs 1
duchess.company.com is up
mail:/var/mail /a/mail/var/mail nfs 1
mail.company.com is up
```

## nfstat

It's easy to monitor the performance of NFS on a UNIX workstation—simply use the nfstat command. This command is available on AIX,

| Table 8.5 amq Options |  |
|---|---|
| Option | Definition |
| -h hostname | Query amd on a different host. |
| -m | Display information on mounted systems. |
| -p | Return the process ID of running amd. |
| -s | Display global statistics. |
| -u mount-point | Expires TTL interval of named mount points. Causes unmount attempt. |

HP-UX, Linux, and Solaris. `nfsstat` provides statistical data on NFS and RPC activity. To display NFS and RPC client information, use `nfsstat -c` (Figure 8.3). The primary indicator is the percentage of invalid NFS/RPC calls. This can be obtained from the `calls` and `badcalls` values for RPC and NFS. The following are some additional indicators you will want to examine:

- `badxids`—The number of acknowledgements from NFS servers with no corresponding outstanding call.
- `timeouts`—The number of times a call timed out waiting for a response from a server.

When the number of timeouts is greater than five percent of calls, you may have a problem in your network or server. If the `badxids` is approximately equal to the `timeouts`, then you probably have a server unable to meet NFS demands. If the `badxids` total is considerably less than `timeouts`, you probably have a network problem and you need to contact your network guru. Linux’s `nfsstat` does not include `badxids` or `timeouts` indicators.

Display NFS server statistics by entering the command `nfsstat -s` (Figure 8.4). Solaris breaks the statistics into version 2 and 3 of NFS. Key indicators include:

- `getattr`—Get file attributes.
- `null`—The number of calls made by the automounter to locate a server for the requested file-system.

![](img/415c89a1ede71e11e5040a0038b6916c_341_0.png)

Figure 8.3 `nfsstat -c` output.
