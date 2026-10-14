H PUX, Linux, and Solaris. `nfsstat` provides statistical data on NFS and RPC activity. To display NFS and RPC client information, use `nfsstat -c` (Figure 8.3). The primary indicator is the percentage of invalid NFS/RPC calls. This can be obtained from the `calls` and `badcalls` values for RPC and NFS. The following are some additional indicators you will want to examine:

+   - `badxids`—The number of acknowledgements from NFS servers with no corresponding outstanding call.
+   - `timeouts`—The number of times a call timed out waiting for a response from a server.

When the number of timeouts is greater than five percent of calls, you may have a problem in your network or server. If the `badxids` is approximately equal to the `timeouts`, then you probably have a server unable to meet NFS demands. If the `badxids` total is considerably less than `timeouts`, you probably have a network problem and you need to contact your network guru. Linux’s `nfsstat` does not include `badxids` or `timeouts` indicators.

Display NFS server statistics by entering the command `nfsstat -s` (Figure 8.4). Solaris breaks the statistics into version 2 and 3 of NFS. Key indicators include:

+   - `getattr`—Get file attributes.
+   - `null`—The number of calls made by the automounter to locate a server for the requested file-system.

![](bbox=[0.247, 0.619, 0.963, 0.929])

Figure 8.3 `nfsstat -c` output.