# CHAPTER 23 Network File System (NFS) 615

| Command Option | Description |
| --- | --- |
| bg | Background mount. Should the mount initially fail (for instance, if the server is down), the mount process will send itself to background processing and continue trying to execute until it is successful. This is useful for file systems mounted at boot time, because the mount command keeps the system from hanging if the server is down. |
| intr | Specifies an interruptible mount. If a process has pending I/O on a mounted partition, this option allows the process to be interrupted and the I/O call to be dropped. For more information, see “The Importance of the intr Option,” later in this chapter. |
| hard | This is an implicit default option. If an NFS file operation has a major timeout, a “server not responding” message is reported on the console and the client continues retrying indefinitely. |
| soft | Enables a soft mount for this partition, allowing the client to time out the connection after a number of retries (specified with the retrans=r option). For more information, see “Soft vs. Hard Mounts,” later in this chapter. |
| retrans=n | The value specifies the maximum number of connection retries for a soft-mounted system. |
| rsize=n | The value is the number of bytes used when reading files from an NFS server. The default value is dependent on the kernel but is currently 4096 bytes for NFSv4. Throughput can be improved greatly by requesting a higher value (for example, rsize=32768). |
| wsize=n | The value specifies the number of bytes used when writing files to an NFS server. The default value is dependent on the kernel but is currently something like 4096 bytes for NFSv4. Throughput can be improved greatly by asking for a higher value (such as wsize=32768). This value is negotiated with the server. |

Table 23-2 Mount Options for NFS