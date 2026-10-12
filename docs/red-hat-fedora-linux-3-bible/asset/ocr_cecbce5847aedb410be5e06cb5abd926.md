must be separated by commas. The following are some options that are valuable for mounting NFS file systems:

+   • **hard** — With this option on, if the NFS server disconnects or goes down while a process is waiting to access it, the process will hang until the server comes back up. This option is helpful if it is critical that the data you are working with not get out of sync with the programs that are accessing it. (This is the default behavior.)

+   • **soft** — If the NFS server disconnects or goes down, a process trying to access data from the server will time out after a set period of time when this is on.

+   • **rsize** — The number of bytes of data read at a time from an NFS server. The default is 1024. Using a larger number (such as 8192) will get you better performance on a network that is fast (such as a LAN) and is relatively error-free (that is, one that doesn’t have a lot of noise or collisions).

+   • **wsize** — The number of bytes of data written at a time to an NFS server. The default is 1024. Performance issues are the same as with the rsize option.

+   • **timeo=#** — Sets the time after an RPC timeout occurs that a second transmission is made, where # represents a number in tenths of a second. The default value is seven-tenths of a second. Each successive timeout causes the timeout value to be doubled (up to 60 seconds maximum). You should increase this value if you believe that timeouts are occurring because of slow response from the server or a slow network.

+   • **retrans=#** — Sets the number of minor retransmission timeouts that occur before a major timeout. When a major timeout occurs, the process is either aborted (soft mount) or a Server Not Responding message appears on your console.

+   • **retry=#** — Sets how many minutes to continue to retry failed mount requests, where # is replaced by the number of minutes to retry. The default is 10,000 minutes (which is about one week).

+   • **bg** — If the first mount attempt times out, try all subsequent mounts in the background. This option is very valuable if you are mounting a slow or sporadically available NFS file system. By placing mount requests in the background, Fedora can continue to mount other file systems instead of waiting for the current one to complete.

> **NOTE:** If a nested mount point is missing, a timeout to allow for the needed mount point to be added occurs. For example, if you mount /usr/trip and /usr/trip/extra as NFS file systems, if /usr/trip is not yet mounted when /usr/trip/extra tries to mount, /usr/trip/extra will time out. Hopefully, /usr/trip will come up and /usr/trip/extra will mount on the next retry.

+   • **fg** — If the first mount attempt times out, try subsequent mounts in the foreground. This is the default behavior. Use this option if it is imperative that the mount be successful before continuing (for example, if you were mounting /usr).