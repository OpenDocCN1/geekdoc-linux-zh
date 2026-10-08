# Chapter 8. Network Interfaces

+   - Set this interface as the default route.
- Do not set this interface as the default route.

DEMAND=<answer>, where <answer> is one of the following:

+   - This interface will allow pppd to initiate a connection when someone attempts to use it.
- A connection must be manually established for this interface.

IDLETIMEOUT=<value>, where <value> is the number of seconds of idle activity before the interface disconnect itself.

INITSTRING=<string>, where <string> is the initialization string passed to the modem device. This option is primarily used with SLIP interfaces.

LINESPE=<value>, where <value> is the baud rate of the device. Possible standard values include here 57600, 38400, 19200, and 9600.

MODEM=<device>, where <device> is the name of the serial device that is used to establish the connection.

MTU=<value>, where <value> is the Maximum Transfer Unit (MTU) for the interface. The MTU refers to the largest number of bytes of a frame can carry, not counting its header information. In some dialup settings, setting this to a value of 576 will result in fewer packets dropped and a slight improvement to the throughput for a connection.

NAME=<name>, where <name> is the reference to the title given to a collection of dialup configurations.

PAPNAME=<name>, where <name> is the name of the Password Authentication Protocol (PAP) exchange that allows you to connect to a remote system.

PEERDNS=<answer>, where <answer> is one of the following:

+   - Modify the system's /etc/resolv.conf file entries to use the DNS servers provided by the remote system when a connection is established.
- The /etc/resolv.conf file will not be modified.

PERSIST=<answer>, where <answer> is one of the following:

+   - This interface should be kept active at all times, even if deactivated by a modem up.
- This interface should not be kept active at all times.

REMIP=<address>, where <address> is the remote system's IP address. This is usually left unspecified.

WVDIALSELECT=<name>, where <name> associates this interface with a dialer configuration in /etc/wvdial.conf. This file contains the phone number to be dialed and other important information for the interface.

# 8.2.3. Other Interfaces

Other interface configuration files use these options include the following: