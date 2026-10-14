two examples, this high availability of swap has consequences for a system that’s not properly configured. The consequences relate to the performance and availability of the cluster itself. This underscores the importance of designing your cluster carefully and thoughtfully considering the applications and the user community that the cluster will be supporting.

Imagine that instead of having each cluster member’s swap partition on the shared bus, it resides on a disk locally accessible to each member. Let’s analyze the pros and cons of this arrangement.

+   - **The pros of having swap on a locally accessible disk:**
+     - The swap-related I/O is not on the shared bus.
+     - The swap-related I/O will not be routed through the cluster interconnect.
+     - The swap activity of one cluster member has little or no impact on any of the other cluster members because the resources involved are no longer shared.
+     - The swap-related I/O is now local to the server that is doing the swapping. From a performance standpoint, this should give better performance.
+   
+   - **The cons of having swap on a locally accessible disk:**
+     - The swap for the cluster member is no longer highly available. If swap is not available for whatever reason (i.e., the HBA fails), the cluster member may crash.
+     - Should a cluster member crash and is down, you will not be able to access the crash dump for that member from any other cluster member. This information would be available only after the cluster member reboots.

Another option to consider is to keep a small primary swap partition on the member boot disk that is large enough to hold a partial dump and add a larger secondary swap partition on a bus that is accessible only to the cluster member.

The decision on where you have each cluster member’s swap partition should ultimately be based on your cluster’s availability criteria. If you decide to have each cluster member’s swap on a local disk, please refer to Chapter 21 on how to implement this.

One last note about the swap partition: regardless of where the primary swap partition physically resides, we recommend that if you are using the eager swap mode algorithm (the default), you should allocate a swap space of at least two to three times the size of the cluster member’s physical memory, which can be distributed on one or more swap partitions. Also, should you later increase the memory of a server, don’t forget to increase the size of the swap space.

If your cluster members are Very Large Memory (VLM)³ systems and used for a specific application like a database, please refer to the application vendor’s documentation on how much swap space is required and which swap algorithm to use. Based on this information, please plan accordingly. If the swap algorithm that you are to use is lazy mode or deferred mode, your swap space requirements can vary widely, from as little as configuring swap to contain only a partial dump to three times the size of memory.

> ³ VLM systems are by definition systems, which utilize 64-bit architecture, multiprocessing, and at least 2 GB of memory for memory intensive applications.