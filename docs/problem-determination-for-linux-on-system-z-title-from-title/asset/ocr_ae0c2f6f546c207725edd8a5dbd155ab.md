![](bbox=[0.26, 0.1, 0.85, 0.55])

Figure 5-31 Disk bottleneck problem determination flow

+   - Storage unit
+     - model
+     - # of rank, # of DA pairs, cache size
+     - configuration of cluster
+   - Connection Type
+     - FICON
+     - FCP
+   - Path
+     - number of path
+     - multipathing (in case of FCP)
+   - LVM configuration
+     - striping
+     - filesystem, raw
+   
+   - Whether processes, which is made to wait by I/O processing, exist or not
+     - This can be found by checking the CPU utilization "iowait"

There are two types of disks used with Linux on System z. One is the traditional mainframe DASD (ECKD™) provisioned using FICON®. The other one is the SCSI disk provisioned using FCP. So, the type of connection (that is, FICON or FCP) needs to be determined. The number of paths for the connection from the System z server to the storage subsystem is also important. In the case of FCP connection, multipathing information must be gathered. At the Linux side, the Logical Volume Manager (LVM) configuration must be examined, if in use. Also, information about the type of file systems or partitions used needs to be gathered.