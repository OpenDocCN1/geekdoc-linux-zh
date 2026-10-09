Remember, you probably didn't choose to install all of those packages. You installed an application like Emacs or Apache or LibreOffice, and that application dragged in all those dependencies. You care only about those dependencies as they affect the software you want. If LibreOffice loses a dependency, you don't want poudriere to build that dependency anymore. Poudriere automatically builds and packages dependencies. All you need to specify is the application you want, and let poudriere do the rest.

Use pkg-query(8) to get a list of all the nonautomatically installed software on one of your production systems.

```
# pkg querry -e '%a=0' %o
www/apache24
shells/bash
sysutils/beadm
---snip---
```

Use this as a base for your package list. Review it for unneeded stuff. Get a similar list from your other production hosts. Use them to assemble your repository's package list.

# ## Poudriere make.conf

Poudriere assembles a unique `make.conf` for each jail from files in `/usr/local/etc/poudriere.d/`. The file `/usr/local/etc/poudriere.d/make.conf` contains the global `make.conf` options that you want set for all of your jails. Other `make.conf` files can override those settings, as discussed in poudriere(8), but we'll focus on per-jail `make.conf` files.

Suppose I want LDAP everywhere across my enterprise. Poudriere's `/usr/local/etc/poudriere.d/make.conf` would contain:

```
OPTIONS_SET=LDAP
```

Hosts running my custom FreeBSD build all use LibreSSL, though. I would create a separate `make.conf` just for that jail, named *amd64-current-make.conf*. It would contain the LibreSSL configuration.

```
DEFAULT_VERSIONS += ssl=libressl
```