# LVM: The Kernel View

In Figure 11-6 we see an overview of the LVM pseudodriver organization within the kernel. As mentioned earlier, an application thread requests a file open by referencing a file system path-name. The virtual file system resolves this to a specific vnode within the kernel file system table. The vnode contains the device number of the file system on which the file is located. The device number for LVM-based file systems directs all I/O requests to the LVM pseudodriver via the kernel's device switch table. Once an I/O request is received by the driver, the driver must pass it through several layers.

![](bbox=[0.27, 0.29, 0.73, 0.57])

**Figure 11-6** The LVM Pseudodriver Architecture

**Strategy Layer:** This layer receives the initial request for a block I/O transaction to a specific file system block. The kernel facilitates this request by passing a buf structure containing the logical volume number (b_dev), request flags defining the transaction (v_flags), the block number within the logical volume (b_blkno), the byte count of the request (b_bcount), and various options (b_options). The strategy layer must validate the request, checking the availability of the requested volume and its size against the block size of the volume.

**Mirror Consistency Layer:** If a logical volume has mirroring configured, then this layer must coordinate mirror writes. A volume may be configured to cache mirrored write request in an MWC. A volume group is divided into logical track groups (LTG) and cached write requests are first registered in one of the MWC's cache records (one per LTG) in kernel memory and also written to an mwc_entry on one of the physical volumes of the volume group. Originally, each volume group had 32 LTGs, but with the 11.1 release this was increased to 126.