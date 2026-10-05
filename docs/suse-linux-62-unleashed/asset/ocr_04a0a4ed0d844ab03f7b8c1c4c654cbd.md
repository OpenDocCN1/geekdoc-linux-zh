# SuSE System Administration
PART III

Another common error encountered while trying to uninstall packages is a dependency error when a package that is being uninstalled has files required by another package. For example, if you try to remove the klibs package from your system, you'll get the following error:

```
error: removing these packages would break dependencies:
klibs is needed by kbase-1.1.1-20
```

This means the package kbase will not function properly if the package klibs (required software libraries) is removed. To remove this package anyway, you can force removal with the --nodeps option to ignore dependency errors.

The other useful option is the --test option, which causes RPM to go through the motions of removing a package without actually removing anything. Usually there is no output from an uninstall, the -vv option is given along with the --test option to see what would happen during an uninstall. For example, the given input (in bold) produces the following output on my system:

```
# rpm -e -vv --klibs
```

produces the following output on my system:

```
D: opening database mode @0x in //var/lib/rpm/
D: dependencies: looking for klibs
D: package kbase require not satisfied: klibs
D: dependencies: looking for libscript.so.2
D: dependencies: looking for libscript.so.2
D: dependencies: looking for libkab.so.2
D: dependencies: looking for libkab.so.2
..
```

```
error: removing these packages would break dependencies:
klibs is needed by kbase-1.1.1-20
```

As you can see, the files that would have been removed are clearly indicated in the output.

# Querying Packages

The Querying mode in RPM allows for determining the various attributes of packages. The following is the basic syntax for querying packages:

```
rpm -q [options] [packages]
```

where options is one or more of the query options listed later in this section. The most basic query is one similar to the following:

```
# rpm -q lx_suse  
```