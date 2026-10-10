If the cblock pool is exhausted, data being passed through a tty or pty device might be lost because no cblock was available when it was needed.

# **nfile**

Set maximum number of files that can be open simultaneously on the system at any given time.

Acceptable Values:
Minimum: “j4”
Maximum: Memory limited
Default: “((16^(NPROC+16+MAXUSERS)/10)+32+2*(NPTY+NSTRPTY+NSTREL))”

Specify integer value or use integer formula expression.

Description
“nfile” defines the maximum number files that can be open at any one time, system-wide.
It is the number of slots in the file descriptor table. Be generous with this number because the required memory is minimal, and not having enough slots restricts system processing capacity.

# **nfilefs**

Specify the maximum combined total number of file locks that are available system-wide to all processes at any given time.

Acceptable Values:
Minimum: “2”
Maximum: Memory limited
Default: “209”

Specify integer value or use integer formula expression.

Description
“nfilefs” gives the maximum number of file/record locks that are available system-wide. When choosing this number, note that one file