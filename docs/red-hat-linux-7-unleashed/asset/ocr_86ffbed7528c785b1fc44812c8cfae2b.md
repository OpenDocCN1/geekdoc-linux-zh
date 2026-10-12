| Method | Meaning |
|---|---|
| `*::*:***:` | The asterisk (*) in this string is representative of an account without a password used for programs that run as a user, but there is no way to log on from a prompt as that user. For example, the *ind* process runs as *news* and retrieves news and stores it in a directory owned by *news* but there is no way to log on as the user *news*. |
| *dns* | Valid only for the *hosts* entry. Lookups are made to the DNS as configured in /etc/resolv.conf. |
| *nis* | Valid for all files. Lookups are made to the NIS server if NIS is active. |
| `[STATUS=action]` | Controls the actions of the Name Service. *STATUS* is one of *SUCCESS* (operation was successful), *NOTFOUND* (record was not found), *UNAVAIL* (selected service was unavailable), or *TRYAGAIN* (service temporarily unavailable, try again). *action* is one of *return* (stop lookup and return current status) or *continue* (continue with next item in this line). For example, a line like `hosts: dns nis [NOTFOUND=return] files` would result in looking up the host first in DNS and then in NIS. Only if neither of these were available would the /etc/hosts file be used. |

This is a typical /etc/nsswitch.conf configured to use the local files for everything, and adds the ability to do DNS-based hostname queries:

```
```text
passwd:		compat

group:		compat
shadow:		compat


hosts:		files dns
networks:	files


protocols:	db files
services:	db files
ethers:	db files
rpc:		db files


netgroup:	db files```
```

With this configuration, all names except network names will be looked up first in /var/db (for efficiency). If not found there, it will be looked up in the corresponding /etc files. There are quite a few databases that could be looked up via NIS if an appropriate entry exists in the corresponding database.