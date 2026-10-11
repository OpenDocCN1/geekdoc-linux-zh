As an example, the following command upgrades the system to the latest version of the RPMs in a particular directory of patches and fixes downloaded from the distribution vendor:

```
rpm -U *.rpm
```

> Remember that the **\-U** and **\-\-upgrade** options both upgrade and install. Therefore, if a package isn't on the system and you invoke it with these options, it is installed, whereas an existing package is upgraded.

Freshening your system is different in one important aspect: If a package is installed and a new package is invoked with the \-F or \-\-freshen option, it is upgraded to the latest version. If that package does not currently exist on the system, it is not upgraded or installed.

As an example, you'd use the following to apply a directory full of .rpm files that contains security patches and fixes to a firewall or other security server:

```
rpm -Fvh *.rpm
```

This feature is useful for local package cache updates, where you've downloaded the latest patches and fixes to a local network resource and want to run scripts on your machines to update them to the latest security releases.

# Removing Packages

Removing a package or set of packages consists of using the \-e or \-\-erase option and requires root access. Removal of packages can be even more fraught with dependency problems than installation because a package can be deeply buried in a tree of dependencies over time.

Removing a package without dependencies is easy. To remove the tarfoo package, you would use the following command:

```
rpm -e tarfoo
```

There's usually no output, the package is removed, and the system returns to the prompt.

The trouble begins when you have multiple packages that all have the same short name, such as tree. With two versions of the tree package on a system, querying the database for the package tree as shown here returns both packages' long format names:

```
rpm -q tree
```