# TABLE 17.3 continued

# NFS mount COMMAND

| Option | Description |
| --- | --- |
| soft | hard | Returns an error if the server does not respond (soft), or continues the retry request until the server responds (hard). If you're using hard, the system appears to hang until the NFS server responds. The default value is hard. |
| intr | nointr | Enables or does not enable keyboard interrupts to kill a process that hangs while waiting for a response on a hard-mounted file system. The default is intr, which makes it possible for clients to interrupt applications that might be waiting for an NFS server to respond. |
| -o | The overlay mount lets the file system be mounted over an existing mount point, making the underlying file system inaccessible. If a mount is attempted on a pre-existing mount point without this flag's being set, the mount fails, producing the error "device busy." |

Here's a note regarding foreground (fg) and background (bg) mounts: File systems mounted with the bg option indicate that mount is to retry in the background if the server's mount daemon (mountd) does not respond when, for example, the NFS server is restarted. From the NFS client, mount retries the request up to the count specified in the retry=<n> option. After the file system is mounted, each NFS request made in the kernel waits a specified number of seconds for a response (specified with the timeo=<n> option). If no response arrives, the timeout is multiplied by two, and the request is retransmitted. If the number of retransmissions has reached the number specified in the retrans=<n> option, a file system mounted with the soft option returns an error, and the file system mounted with the hard option prints a warning message and continues to retry the request. Sun recommends that file systems