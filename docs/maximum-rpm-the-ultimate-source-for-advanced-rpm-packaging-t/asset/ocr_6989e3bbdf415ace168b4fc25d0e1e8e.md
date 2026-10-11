Appendix B    The rpmrc File 355

```
```text
ppq_path       : (not set)
require_distribution : (not set)
require_icon     : (not set)
require_vendor   : (not set)
root           : (not set)
rpmdir         : /usr/src/redhat/RPMS
signature      : none
sourcedir      : /usr/src/redhat/SOURCES
specdir        : /usr/src/redhat/SPECS
srcrpmdir      : /usr/src/redhat/SRPMS
timecheck      : (not set)
tmpath         : /var/tmp
topdir         : /usr/src/redhat
vendor         : (not set)
#
```
```

As you can see, the `--showrc` option clearly displays the values RPM will use. `--showrc` can also be used with the `--rcfile` option, which makes it easy to see the effect of specifying a different `rpmrc` file.

# ## B.2. Different Places an rpmrc File Resides

RPM looks for `rpmrc` files in four places:

+   - In `/usr/lib/`, for a file called `rpmrc`
+   - In `/etc/`, for a file called `rpmrc`
+   - In a file called `.rpmrc` in the user's login directory
+   - In a file specified by the `--rcfile` option, if the option is present on the command line

The first three files are read in the order listed, such that if a given `rpmrc` entry is present in each file, the value of the entry read last is the one used by RPM. This means, for example, that an entry in `.rpmrc` in the user's login directory will always override the same entry in `/etc/rpmrc`. Likewise, an entry in `/etc/rpmrc` will always override the same entry in `/usr/lib/rpmrc`.

If the `--rcfile` option is used, then only `/usr/lib/rpmrc` and the file following the `--rcfile` option are read, in that order. The `/usr/lib/rpmrc` file is always read first. This cannot be changed.

Let's look at each of these files, starting with `/usr/lib/rpmrc`.

# ### B.2.1. /usr/lib/rpmrc

The file `/usr/lib/rpmrc` is always read. It contains information that RPM uses to set some default values. This file should never be modified! Doing so may cause RPM to operate incorrectly.