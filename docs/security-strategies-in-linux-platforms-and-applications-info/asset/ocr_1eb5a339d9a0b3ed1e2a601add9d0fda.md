# CHAPTER 11 | Managing Security Alerts and Updates

The update (and related) option is powerful when updating a series of packages for a system. For example, the following command checks connected repositories for available updates:

```
# yum check-update
```

If the list of available updates is satisfactory, you can download and install all updates with the following command:

```
# yum update
```

If you want to exclude a package from the list of updates, the --exclude switch can help. For example, the following command excludes the noted packages from an update:

```
# yum update --exclude=samba, samba-common, samba-client
```

Of course, the yum command can be used to uninstall a package, with dependencies. For example, the following command removes the Samba server with any dependent packages:

```
# yum remove samba
```

You can also take advantage of how packages are organized on Red Hat distributions. For example, the following command lists available package groups:

```
# yum groupplist
```

List of Commands:

+   check-update Check for available package updates
clean Remove cached data
deplist List a package's dependencies
downgrade downgrade a package
erase Remove a package or packages from your system
groupinfo Display details about a package group
groupinstall Install the packages in a group on your system
list List groups
groupremove Remove the packages in a group or of groups
help Display a helpful usage message
info-security Returns security data for the packages listed, that affects your system
install Install a package or packages on your system
list List groups of packages
list-security Returns security data for the packages listed, that affects your system
local Install a local RPM
makecache Display the metadata cache
provide Find what package provides the given value
reinstall reinstall a package
display the configured software repositories
resolve which package provides the given dependency
search Search details for the given string
shell Run an interactive shell
udate Update a package or packages on your system
update-minimal Works like update, but goes to the 'newest' package match which fixes a problem that affects you
upgrade Update taking obsoletes into account

FIGURE 11-2

*The yum command is powerful.*