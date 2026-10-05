```
$ aptitude nfs-common
Package: nfs-common
State: not installed
Version: 1.1.2.0-ubuntu4
Priority: optional
Section: net
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Size: 602k
Depends: portmap (>= 6.0-10ubuntu1), adduser, ucf, lsb-base (>=
1.3-ubuntu3), netbase (>= 4.24), libproc6 (>= 2.4), libcommer2 (>= 1.01),
libweent-1.4-2 (>= 1.4-13), libgapi-krb5-2 (>=
1.6.dsfg2), libsqsgue1, libscrypt3 (>= 1.6.dsfg2),
libkrb5-3 (>= 1.6.dsfg2), libnfsidmap2, libprpcsecgss3,
libwrap0 (>= 7.6-4), upstart-job
```

Replaces: (mount >= 2.1.3)

Upstream: Sourceforge "nfs", CVS module nfs-utils.
Homepage: http://nfs.sourceforge.net/

# apt-cache: DISPLAYS PACKAGE INFORMATION

The apt-cache utility has commands—some manipulate the APT package cache and others display information about packages in the cache. This section contains examples of some of the simpler commands that display information. Use apt-file (page 521) to display information about packages that are not installed on the system.

Displaying package apt-cache depends command displays the list of packages that a package depends on. These are forward (normal) dependencies. Use the --recurse option to display the packages that the dependencies are dependent on (the dependencies' dependencies).

```
$ apt-cache depends nfs-common
nfs-common
Depends: portmap
Depends: adduser
Depends: ucf
```

```
Conflicts: <nfs-client>
Replaces: mount
Replaces: <nfs-client>
nfs-common
Replaces: nfs-kernel-server
```

The rdepends apt-cache command displays the list of packages that are dependent on a specified package. These are reverse dependencies. Use the --recurse option to display packages that are dependent on the dependent packages.