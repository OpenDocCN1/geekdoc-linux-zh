data to the disks is stored in the NVS (nonvolatile storage) in the *opposite* cluster node. Each of the two cluster nodes has a high-performance cache that can be configured with 3GB, 4GB, 8GB, 16GB, or 32GB of Synchronous Dynamic RAM (SDRAM) that provides single-bit, double-bit error detection. The ESS realizes full redundancy with dual power supplies, dual cooling fans, dual battery backup, and dual machines controlling the ESS. Communications are handled to the servers through host bus adapters (HBAs) and to the disk storage through device adapters (DAs) pairs. The clustered configuration allows for failover in the event of a cluster node failure. In this event, the ESS takes corrective action and transfers control to the surviving node in the cluster. The result is no interruption in service and no data loss.

The ESS supports using mixed drive sizes (intermix) in 8-packs. These 8-packs must be added to the ESS in pairs. Intermix support is available on all ESS models and provides for many different configuration options.

The ESS requires careful configuration planning. It is extremely important that you take your time planning the layout of data and give careful consideration of LUN sizes. The LUNs can be configured to just about any size that you want to use. Depending on your application and platform, this decision will vary. These are the basic steps to start your configuration:

+   - Draw a map that represents a logical view of how you want the ESS laid out.
+   - Use the logical view to map to the physical devices within the ESS.
+   - Ensure that you have done your homework for the required store capacity for current and future storage needs.
+   - Document your layout so that it is easy to understand when you configure the ESS using the StorWatch Specialist.

Let's go on to look at what the StorWatch Specialist and Expert can do.

# ## ESS StorWatch Specialist

The ESS StorWatch Specialist is a Web browser-based interface for configuring and controlling the ESS. In fact, you can control many Sharks from a single Specialist session. The capabilities of the StorWatch Specialist and its look and feel are completely dependent upon the LIC. If you have a back level of the Licensed Internal Code, you may not be able to exercise some options. An example is the ability to mix different drive sizes within the same ESS. With the ESS Specialist, you can conduct the following tasks:

+   - Show the status of the ESS
+   - Monitor the ESS error logs
+   - Create and modify RAID and JBOD (just a bunch of disks) ranks
+   - Show the Licensed Internal Code (LIC) version level