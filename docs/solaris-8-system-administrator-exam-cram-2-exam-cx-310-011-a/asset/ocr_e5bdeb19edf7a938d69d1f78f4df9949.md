# SPARC

A computer architecture developed by Sun Microsystems. It uses a reduced instruction set processor, which provides superior performance over processors that operate using a standard instruction set.

# standalone system

A system that uses local disk space to store all operating system files, applications, and user data, including the root (/), /usr, /export/home, and /var file systems. Likewise, a standalone system provides local swap space for the system’s virtual memory. A standalone system can function autonomously and can be networked or non-networked.

# sticky bit

A special file permission that, when set on a directory allowing write permission for everyone, permits only the user account that created the files and subdirectories under that directory to remove those files and subdirectories. A sticky bit is especially useful for the /tmp directory, which is available from any user account. The sticky bit permission has an absolute mode of 1000 and a symbolic mode of t.

# striped virtual device

A device consisting of two or more slices. The slices can be on the same physical disk or on several physical disks. The slices also can be different sizes. They are addressed in an interleaved manner. That is, as space is needed, it is allocated as a

block from the first slice, then a block from the second slice, and so on.

# subdisk

The basic unit Volume Manager uses to allocate storage. A subdisk is a portion of the public region of a VM disk.

# SunInstall

An interactive Open Windows installation program that can be used to install the Solaris 8 software but does not support installation of co-packaged software.

# superuser

A special administrative account (“root”) that provides the ultimate in terms of access to data and services because it can override any file permissions on the system.

# swap space

Disk space used as virtual memory. Swap space can be on a local disk or on a remote disk that is accessed via the network.

# syslog

A facility used to collect messages from system programs and applications. These messages are identified by a source facility and priority level. The /etc/syslog.conf file assigns an action to each combination of source and priority level.

# syslog actions

The action that should be performed when the syslogd daemon receives a syslog message of the identified source.priority.