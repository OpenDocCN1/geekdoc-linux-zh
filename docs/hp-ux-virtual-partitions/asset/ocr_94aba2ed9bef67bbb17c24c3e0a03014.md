+   - Host Name
+   - Internet Address
+   - Subnet Mask (this is optional)
+   - Station Address in hex or client ID (this is optional)
+   - Boot File Name
+   - Whether you’ll be using Ethernet or IEEE 802.3 for booting
+   - Whether to send the hostname to the client or device

You can select Enable Protocol Server or Disable Protocol Server from the Actions menu, depending on whether your system is currently disabled or enabled to support this functionality. When you Enable Protocol Server, you also enable Trivial File Transfer Protocol (TFTP), which boot devices use to get boot files. When you enable or disable this, the /etc/inetd.conf is edited. This file contains configuration information about the networking services running on your system. If a line in /etc/inetd.conf is preceded by a “#”, then it is viewed as a comment. The daemon that reads the entries in this file is /usr/sbin/inetd. Before enabling or disabling Boot, you may want to view the /etc/inetd.conf file and see what services are enabled. After you make your change through SAM, you can again view /etc/inetd.conf to see what has been modified. See System Access for security related to /etc/inetd.conf. The following is the beginning of the /etc/inetd.conf file from a system showing Boot and TFTP enabled. Also, a brief explanation of the fields in this file appears at the beginning of the file:

```
```
## Configured using SAM by root
##

# Inetd reads its configuration information from this file upon ex-
# ecution and at some later time if it is reconfigured.
#
# A line in the configuration file has the following fields separated
# by tabs and/or spaces:
#
# service name          as in /etc/services
# socket type           either "stream" or "dgram"
# protocol              as in /etc/protocols
# wait/nowait           only applies to datagram sockets, stream
#                       sockets should specify nowait
# user                  name of user as whom the server should run
# server program        absolute pathname for the server inetd
#                       will execute
# server program args.  arguments server program uses as they
```
```