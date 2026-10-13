```
shadow:      files nis
hosts:       nis files dns

services:    nis [NOTFOUND=return] files
networks:    nis [NOTFOUND=return] files
protocols:   nis [NOTFOUND=return] files
rpc:         nis [NOTFOUND=return] files
ethers:      nis [NOTFOUND=return] files
netmasks:    nis [NOTFOUND=return] files
netgroup:    nis [NOTFOUND=return] files
bootparams:  nis [NOTFOUND=return] files
publickey:   nis [NOTFOUND=return] files
automount:   files nis
aliases:     nis [NOTFOUND=return] files
```

In this file, several entries deserve attention to highlight the way the file works. Consider the following entry:

```
passwd:   files nis
```

This entry says that user lookup should first be performed against the local `/etc/passwd` file and, if the user is not found, then user lookup should be performed against the NIS user database. By contrast, consider the following entry:

```
hosts:    nis files dns
```

This entry indicates that hostname lookups should first be done against the NIS host database. If a matching entry is not found, then the local `/etc/hosts` file should be consulted. If a host is still not found, then a DNS query should be attempted to resolve the hostname into an address.

The following entry

```
services:  nis [NOTFOUND=return] files
```

is an example of several entries containing `[NOTFOUND=return]`. This indicates that the lookup should only continue from the relevant NIS database map to the relevant file in `/etc` when the NIS lookup fails for a reason other than a lack of a match in the database.

For instance, if you attempt a lookup and a matching entry is not found in the NIS database, then the lookup fails and stops. But if you attempt a lookup and the request to the NIS server times out, then the lookup continues with the local file in `/etc`.

# Useful Scripts

NIS management can be eased by the creation of several administrative scripts. In particular, it is useful to use a script for adding and removing servers from an NIS domain. The following script, `add-rm-ypservers`, eases this management task.