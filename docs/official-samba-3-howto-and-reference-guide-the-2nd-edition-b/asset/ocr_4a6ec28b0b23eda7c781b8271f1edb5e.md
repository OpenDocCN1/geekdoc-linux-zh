# ### 31.2.2.4 Restrictive Constraints on Distributed File Systems

Where a clustered server provides purely SMB services, oplock handling may be done within the server pool without imposing a need for this to be passed to the backend file system pool.

On the other hand, where the server pool also provides NFS or other file services, it will be essential that the implementation be oplock-aware so it can interoperate with SMB services. This is a significant challenge today. A failure to provide this interoperability will result in a significant loss of performance that will be sorely noted by users of Microsoft Windows clients.

Last, all state information must be shared across the server pool.

# ### 31.2.2.5 Server Pool Communications

Most backend file systems support POSIX file semantics. This makes it difficult to push SMB semantics back into the file system. POSIX locks have different properties and semantics from SMB locks.

All smbd processes in the server pool must of necessity communicate very quickly. For this, the current tdb file structure that Samba uses is not suitable for use across a network. Clustered smbd s must use something else.

# ### 31.2.2.6 Server Pool Communications Demands

High-speed interserver communications in the server pool is a design prerequisite for a fully functional system. Possibilities for this include:

+   - Proprietary shared memory bus (example: Myrinet or SCI [scalable coherent interface]). These are high-cost items.
+   - Gigabit Ethernet (now quite affordable).
+   - Raw Ethernet framing (to bypass TCP and UDP overheads).

We have yet to identify metrics for performance demands to enable this to happen effectively.

# ### 31.2.2.7 Required Modifications to Samba