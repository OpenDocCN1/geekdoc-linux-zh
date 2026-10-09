| File | Map | Description |
|:---|:---|:---|
| /etc/passwd | passwd.byname, passwd.byuid | Maps an encrypted password to the respective user login name. |
| /etc/group | group.byname, group.bygid | Maps GIDs to group names. |
| /etc/services | services.byname, services.bynumber | Maps service description to a service name. |
| /etc/rpc | rpc.byname, rpc.bynumber | Maps RPC service numbers to the corresponding RPC service names. |
| /etc/protocols | protocols.byname, protocols.bynumber | Maps protocol numbers to protocol names. |
| /usr/lib/aliases | mail.aliases | Maps mail aliases to mail alias names. |

# The securenets file

NIS will listen to all networks after the installation of the daemons: *ypserv*, and *ypxfrd*. Both the daemons restrict user access by using the */var/yp/securenets* file. The securenets file contains only the range of IP addresses to which the daemons have to respond. By default, the NIS will listen to all networks after the installation of daemons where the securenets file remains empty. You can add the specific range of IP addresses to the file so that the daemons will respond only to those networks.

# The netgroup File

The netgroup file contains a list of user groups on the network along with their permissions. This helps in checking the permissions while performing remote mounts and working in remote logins and remote shells. The user groups are defined in the format:

```
Groupname member1, [member 2....]
```

where *member1* refers to another group name, which consists of three fields. They are hostname, user name, and domain name. For example, a group named *systems* is defined as `systems (analytical, cwarden, ourglobalcompany)`, where *analytical* refers to the hostname, *cwarden* refers to the user name, and *ourglobalcompany* refers to the domain name. If any of the fields are left empty, then it is considered as the wildcard. For example, in a group defined as `systems (analytical, -, ourglobalcompany)`, the host *analytical* belongs to the group *systems* in the domain *ourglobalcompany* but there are no users for this group.

# Information About NIS Maps

Any NIS user can display information about NIS maps. The following table lists the commands that are used to display the maps.

| Command | Enables You To |
|:---|:---|
| `ypcat map name or its alias` | List the values in a map. |
| `ypmatch -x` | List the aliases of maps. |
| `ypwhich -m` | List the available maps and the master server names. |