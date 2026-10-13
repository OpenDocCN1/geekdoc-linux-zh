# Table 36-2: NFS Mount Options

| Options | Description |
|---|---|
| retrans=n | The number of retransmissions or minor timeouts for an NFS mount operation before a major timeout (default is 3). At that time, the connection is cancelled or a 'server not responding' message is displayed. |
| soft | Mount system using soft mount. |
| hard | Mount system using hard mount. This is the default. |
| intr | Allow NFS to interrupt the file operation and return to the calling program. The default is not to allow file operations to be interrupted. |
| bg | If the first mount attempt times out, continue trying the mount in the background. The default is to fail without backgrounding. |
| tcp | Mount the NFS file system using the TCP protocol, instead of the default UDP protocol. |