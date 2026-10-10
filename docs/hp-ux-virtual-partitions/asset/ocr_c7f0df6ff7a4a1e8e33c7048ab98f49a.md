```
tty        1  0/0/5/0     agio0        CLAIMED      INTERFACE      PCI Serial (103c1048)
ba         2  1/1         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ba         2  2/2         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ba         3  0/3         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ian        1  0/3/3/0     bclan        CLAIMED      INTERFACE      HP ASIO/A65580B PCI 10/100Base-TX Adaptor
ba         4  0/4         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ext_bus    4  0/4/0/0     c720         CLAIMED      INTERFACE      SCSI Fast Wide Differential
target     7  0/4/0/0.7   tgt          CLAIMED      DEVICE
ctl        7  0/4/0/0.7   sctl         CLAIMED      DEVICE         Initiator
ext_bus    5  0/4/0/1     c720         CLAIMED      INTERFACE      SCSI CB75 Fast
Wide differential
target     8  0/4/0/1.7   tgt          CLAIMED      DEVICE
ctl        5  0/4/0/1.7   sctl         CLAIMED      DEVICE         Initiator
ba         5  0/5         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ba         6  0/6         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ba         7  0/7         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ext_bus    6  0/7/0/1     c720         CLAIMED      INTERFACE      SCSI CB75 Fast Wide Differential
target     9  0/7/0/0.7   tgt          CLAIMED      DEVICE
ctl        6  0/7/0/0.7   sctl         CLAIMED      DEVICE         Initiator
ext_bus    7  0/7/0/1     c720         CLAIMED      INTERFACE      SCSI CB75 Fast Wide Differential
target    10  0/7/0/1    tgt          CLAIMED      DEVICE
ctl        7  0/7/0/1.7   sctl         CLAIMED      DEVICE         Initiator
memory       0  8          memory       CLAIMED      MEMORY         Memory
processor    0  160       processor    CLAIMED      PROCESSOR      Processor
processor    1  166       processor    CLAIMED      PROCESSOR      Processor
```

I normally run ioscanc with the -f option because it includes the *Driver*, *S/W State*, and *H/W Type* columns. I am interested in the driver associated with the hardware in the system that the -f option produces.

The ioscanc output shows all of the hardware that comprises the system, including the two processors in the system.

The file /stand/vmunix is the currently running kernel. Here is a long listing of the directory /stand on the L-Class system, which shows the file /stand/vmunix:

```
# lg -1
total 74274
drwxr-xr-x   4 root     sys      2048 Aug 25 11:24 ddtk
lrwxr-xr-x   5 root     sys      1024 Aug 29 14:25 ddsm.vmunix.prev
-rw-r-----   1 root     sys      3024 Aug 4 12:26 iocconf
-r----r----   1 root     sys       82 Aug 4 12:27 kernel
drwxr-xr-x   2 root     root     1024 Aug 29 11:33 krs
drwxr-xr-x   2 root     root     1024 Aug 29 11:33 krs.lkg
drwxr-xr-x   2 root     root     1024 Aug 29 11:39 krs.tmp
drwxr-xr-x   2 root     root     8192 Aug 4 11:36 lost+found
-rw-------   1 root     root       12 Aug 29 11:33 rootconf
lrwxr-xr-x   1 root     sys      1180 Aug 24 12:52 system
drwxr-xr-x   2 root     root     1026 Aug 4 12:21 system.prev
drwxr-xr-x   1 root     sys     14774416 Aug 24 12:53 vmunix
```