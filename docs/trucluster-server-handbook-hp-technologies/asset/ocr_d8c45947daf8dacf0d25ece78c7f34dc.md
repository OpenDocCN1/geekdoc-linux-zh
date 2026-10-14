Now that we have shown how you can differentiate a member-specific file from a cluster-common file, it bears mentioning that for every rule there is an exception. In other words, this is not the only way that member-specific files exist. Another method (although much less common) of creating a member-specific file is instead of placing the file in a member-specific directory and creating a CDSL to it, simply rename the file with a unique extension. An example of this second method is provided in Chapter 16 where the Cluster Alias subsystem is described. The Cluster Alias subsystem uses gated.conf files by creating a member-specific gated.conf file and appending "membern" to the file name (e.g. /etc/gated.conf.member1).

# 6.1.2 Is it in rc.config or rc.config.common?

We mentioned earlier that configuring a network interface was a member-specific task and that configuring NIS was a cluster-wide task, so how is this implemented in our rc.config files? Since NIS is configured cluster-wide, then all the NIS variables should be in /etc/rc.config.common, but not in /etc/rc.config.

```
# grep NIS /etc/rc.config
<nothing is returned>
```

```
# grep NIS /etc/rc.config.common
NIS_DOMAIN="DAN"
export NIS_DOMAIN
NIS_CONF="YES"
export NIS_CONF
NIS_TYPE="CLIENT"
export NIS_TYPE
NIS_ARGS="-s -S DAN, bacon.dec.com, gravy.dec.com"
export NIS_ARGS
```

The next question you might be asking is, "In what order are these files being called during startup?" In order to avoid unnecessary changes, since many of the init scripts already called rc.config, it was decided that rc.config would call rc.config.common.

```
# cat /etc/rc.config
#!/bin/sh
#
# Read in the cluster attributes before overriding them with the member
# specific options.
. /etc/rc.config.common
...
```