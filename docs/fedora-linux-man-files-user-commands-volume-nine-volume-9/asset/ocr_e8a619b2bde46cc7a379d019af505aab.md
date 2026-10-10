# SOCKETS AND FIFOS

/run/systemd/notify

Daemon status notification socket. This is an **AF_UNIX** datagram socket and is used to implement the daemon notification logic as implemented by (3).

/run/systemd/private

Used internally as commnication channel between (1) and the systemd process. This is an **AF_UNIX** stream socket. This interface is private to systemd and should not be used in external projects.

/dev/initctl

Limited compatibility support for the SysV client interface, as implemented by the systemd-initctl.service unit. This is a nad pipe in the file system. This interface is obsolete and should not be used in new applications.