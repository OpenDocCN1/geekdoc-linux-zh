acdirmin=n (attribute cache directory file minimum) The n is the number of seconds, at a minimum, that NFS waits before refreshing directory file attributes (default is 30 seconds).

acregmax=n (attribute cache regular file maximum) The n is the number of seconds, at a maximum, that NFS waits before refreshing regular file attributes (default is 60 seconds).

acregmin=n (attribute cache regular file minimum) The n is the number of seconds, at a minimum, that NFS waits before refreshing regular file attributes (default is 3 seconds).

actimeo=n (attribute cache timeout) Sets acregmin, acregmax, acdirmin, and acdirmax to n seconds (without this option, each individual option takes on its assigned or default value).

# ## Error Handling

The following options control what NFS does when the server does not respond or when an I/O error occurs. To allow for a mount point located on a mounted device, a missing mount point is treated as a timeout.

fg (bg) (foreground) Retries failed NFS mount attempts in the foreground (default). The bg (background) option retries failed NFS mount attempts in the background.

hard (soft) Displays server not responding on the console on a major timeout and keeps retrying (default). The soft option reports an I/O error to the calling program on a major timeout. In general, it is not advisable to use soft. As the mount man page says of soft, “Usually it just causes lots of trouble.” For more information refer to “Improving Performance” on page 734.

nointr (intr) (no interrupt) Does not allow a signal to interrupt a file operation on a hard- mounted directory hierarchy when a major timeout occurs (default). The intr option allows this type of interrupt.

retrans=n (retransmission value) After n minor timeouts, NFS generates a major timeout (default is 3). A major timeout aborts the operation or displays server not responding on the console, depending on whether hard or soft is set.

retry=n (retry value) The number of minutes that NFS retries a mount operation before giving up (default is 10,000).

timeo=n (timeout value) The n is the number of tenths of a second that NFS waits before retransmitting following an RPC, or minor, timeout (default is 7). The value is increased at each timeout to a maximum of 60 seconds or until a major timeout occurs (see retrans). On a busy network, in case of a slow server, or when the request passes through multiple routers/gateways, increasing this value may improve performance.

# ## Miscellaneous Options

Following are additional useful options:

lock (no lock) Permits NFS locking (default). The no lock option disables NFS locking (does not start the lockd daemon) and is useful with older servers that do not support NFS locking.

mounthost=name The name of the host running mountd, the NFS mount daemon.