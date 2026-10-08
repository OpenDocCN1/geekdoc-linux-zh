# 36 Chapter 4. The sysconfig Directory

# 4.1.20. /etc/sysconfig/mouse

The /etc/sysconfig/mouse file is used to specify information about the available mouse. The following values may be used:

+   - FULLNAME=<value>, where <value> refers to the full name of kind of mouse being used.
- MOUSETYPE=<value>, where <value> is one of the following:
  - imps2 — A generic USB mouse.
  - microsoft — A Microsoft™ mouse.
  - mouseman — A MouseMan™ mouse.
  - mysystems — A Mouse Systems™ mouse.
  - ps/2 — A PS/2 mouse.
  - msbm — A Microsoft™ bus mouse.
  - logibm — A Logitech™ bus mouse.
  - atbim — An ATim bus mouse.
  - logitech — A Logitech™ mouse.
  - mmseries — An older MouseMan™ mouse.
  - mmittab — An mhmittab mouse.

+   - XEM3=<value>, where <value> is one of the following boolean values:
- yes — The mouse has two buttons, but three buttons must be enabled.
- no — The mouse has three buttons.

+   - XMOUSETYPE=<value>, where <value> refers to the kind of mouse used when X is running. The options are the same as the MOUSETYPE setting in this file.
- DEVICE=<value>, where <value> is the mouse device.
In addition, /dev/mouse is a symbolic link to the actual mouse device.

/etc/sysconfig/named
The /etc/sysconfig/named file is used to pass arguments to the named daemon at boot time. The named daemon is a Domain Name System (DNS) server which implements the Berkeley Internet Domain Name (BIND) version 9. This server maintains a table of which hostnames are associated with IP addresses on the network.
Currently, the following values may be used:

+   - ROOTDIR="<some/where>", where <some/where> refers to the full directory path of a configured environment which named runs. The chroot info must be configured.
- OPTIONS="<value>", where <value> is any option in the man page for named except -t. In place of -t, use the ROOTDIR line above.

For more information about what parameters are available for this file, the named man page. For detailed information on how to configure a BIND DNS server, see Chapter 12 Berkeley Internet Name Domain (BIND). By default, the file contains no parameters.