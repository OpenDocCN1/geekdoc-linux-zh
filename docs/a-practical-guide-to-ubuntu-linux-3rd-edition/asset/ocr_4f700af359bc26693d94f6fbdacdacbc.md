the attribute cache of an NFS-mounted file to determine whether another process has modified the file. This period is specified as a minimum and maximum number of seconds for ordinary and directory files. Following is a list of options that affect attribute caching:

**ac**(**noac**) (attribute cache) Permits attribute caching (default). The **noac** option disables attribute caching. Although **noac** slows the server, it avoids stale attributes when two NFS clients actively write to a common directory hierarchy.

**acdirmax**=n (**attribute cache directory file maximum**) The n is the number of seconds, at a maximum, that NFS waits before refreshing directory file attributes (default is 60 seconds).

**acdirmin**=n (**attribute cache directory file minimum**) The n is the number of seconds, at a minimum, that NFS waits before refreshing directory file attributes (default is 30 seconds).

**acregmax**=n (**attribute cache regular file maximum**) The n is the number of seconds, at a maximum, that NFS waits before refreshing regular file attributes (default is 60 seconds).

**acregmin**=n (**attribute cache regular file minimum**) The n is the number of seconds, at a minimum, that NFS waits before refreshing regular file attributes (default is 3 seconds).

**actimeo**=n (**attribute cache timeout**) Sets **acregmin**, **acregmax**, **acdirmin**, and **acdirmax** to n seconds (without this option, each individual option takes on its assigned or default value).

# ERROR HANDLING

The following options control what NFS does when the server does not respond or when an I/O error occurs. To allow for a mount point located on a mounted device, a missing mount point is treated as a timeout.

**fg**(**bg**) (foreground) Retries failed NFS mount attempts in the foreground (default). The **bg** (background) option retries failed NFS mount attempts in the background.

**hard**(**soft**) Displays **NFS server not responding** on the console on a major timeout and keeps retrying (default). The **soft** option reports an I/O error to the calling program on a major timeout. In general, it is not advisable to use **soft**. As the mount man page says of **soft**, "Usually it just causes lots of trouble." For more information refer to "Improving Performance" on page 780.

**nointr**(**intr**) (**no** interrupt) Does not allow a signal to interrupt a file operation on a hard-mounted directory hierarchy when a major timeout (see retrans) occurs (default). The **intr** option allows this type of interrupt.

**retrans**=n (**retransmission value**) After n minor timeouts, NFS generates a major timeout (default is 3). A major timeout aborts the operation or displays **server not responding** on the console, depending on whether **hard** or **soft** is set.

**retry**=n (**retry value**) The number of minutes that NFS retries a mount operation before giving up (default is 10,000).

**timeo**=n (**timeout value**) The n is the number of tenths of a second that NFS waits before retransmitting following an RPC, or minor, timeout (default is 7). The value is