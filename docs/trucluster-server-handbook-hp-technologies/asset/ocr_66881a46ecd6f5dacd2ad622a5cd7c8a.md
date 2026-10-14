![](bbox=[0.162, 0.091, 0.839, 0.506])

# Table 23-2: CAA Components EVM Event Subscription

Note that as of V5.1A, there exists a resource monitor registry (caa_type.reg) where resource monitors are registered with the resource manager. This registry is a text file but do not attempt to edit it.

The resource monitor registry does contain non-printable characters within it, so to see what resource monitors are within the caa_type.reg file, we recommend using the strings(1) command.

```
```text
$ strings /var/cluster/caa/registry/caa_type.reg
application application.so SCRIPTPATH=/var/cluster/caa/script
network network.so NONE
tape tape.so NONE
changer changer.so NONE
```
```

The changer, tape, and network resource monitors subscribe to EVM events in order to know when the monitored hardware component has failed or has become available (see Table 23-2).

# 23.3.4  Resource Registry Database

The resource registry database is located in the /var/cluster/caa/registry directory. The file name may differ depending on the version of the TruCluster Server software that is installed but starts with “caa.reg”.