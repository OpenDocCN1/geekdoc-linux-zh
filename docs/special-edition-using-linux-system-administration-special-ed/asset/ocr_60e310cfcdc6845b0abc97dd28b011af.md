```
```text
global
comment "very important partitions on fast machines"
compress client best
priority high
}
define dumptype ncomp-high {
comp-high
comment "very important partitions on slow machines"
compress none
}
define dumptype ncomp-test {
global
comment "test dump without compression, no /etc/dumpdates recording"
compress none
record no
priority medium
}
define dumptype comp-test {
ncomp-test
comment "test dump with compression, no /etc/dumpdates recording"
compress client fast
}
# network interfaces
#
# These are referred to by the disklist file.  They define the attributes
# of the network interface that the remote machine is accessed
# through.
# Notes: - netusage above defines the attributes that are used when
#          the disklist entry doesn't specify otherwise.
#        - the values below are only samples.
#        - specifying an interface does not force the traffic to
#          pass through that interface. Your OS routing tables do
#          that. This is just a mechanism to stop Amanda trashing your
#          network.
# Attributes are:
#   use          - bandwidth above which amanda won't start
#                  backups using this interface. Note that if
#                  a single backup will take more than that,
#                  amanda won't try to make it run slower!
define interface local {
comment "a local disk"
use 1000 kbps
}
define interface le0 {
comment "10 Mbps ethernet"
use 400 kbps
}
# You may include other amanda configuration files, so you can share
# dumptypes, tapetypes and interface definitions among several
# configurations.
#include "/usr/local/amanda.conf.main"
```
```

Several entries in this file bear further analysis because you will need to customize them for your site. These are outlined in Table 10.2.