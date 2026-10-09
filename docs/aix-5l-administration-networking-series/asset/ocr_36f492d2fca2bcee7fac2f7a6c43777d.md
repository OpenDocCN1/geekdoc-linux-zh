The most interesting part of this Shark is that support for RAID 0+1 is added to the RAID 5 disk configuration options in coming releases. The result of the enhancements made to the ESS is twofold. For heavy storage requirements, a performance boost of up to two times is seen. This value will not be so great if your storage demands are not stressing the current model. I am guessing that this model will be called the G10/G20, since the last models were E and F, but I may be wrong.

# Host Bus Adapters

Communications between the servers and the ESS is done through *host bus adapters (HBAs)*. You have four choices in HBA adapters, ESCON, FICON, Fibre Channel, or SCSI. Each server can have multiple connections spread across the host adapter bays. This not only provides better availability to the server in case you lose an HBA bay, but it also spreads the I/O across all of the adapters. This is done automatically if you install the *Data Path Optimizer / Subsystem Device Driver* on the server. Up to 16 HBAs can be installed, except for Fibre Channel, which can support up to 8 dual-port HBAs.

# Data Path Optimizer / Subsystem Device Driver (SDD)

The Data Path Optimizer / Subsystem Device Driver (SDD), for the open systems environment, enables multiple Fibre Channel and SCSI paths from the server to the target LUN group. The SDD optimizes the workload across all of the available HBA paths. This improves the server I/O by allowing parallel access to the same data, which balances the load. The SDD is a pseudo-device driver that resides on the server and provides the following functions:

+   • Dynamic load balancing of I/O across multiple paths
+   
+   • Enhanced data availability
+   
+   • Failover protection in multipath environments

The SDD adds another layer to the protocol stack and provides dynamic path protection by path monitoring and selection for data flow and load balancing, which eliminates data-flow bottlenecks between the server and the ESS.

The SDD supports AIX tracing. The **trace** ID for SDD is 2F8 and is used in the following manner:

**To Start SDD Tracing**

```
# trace -a -j 2F8
```

**To Stop the Tracing**

```
# tracstop
```

**To Read the Trace Report**

```
# trcrpt | more
```