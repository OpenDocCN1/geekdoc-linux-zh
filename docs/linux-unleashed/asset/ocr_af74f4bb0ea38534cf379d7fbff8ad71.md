The router component of smail handles the resolution of destination addresses, routing to the next mail host for further forwarding, and determination of which transport should be used to send the message on. The router component performs a number of tasks, first determining whether the message is for a local or remote machine (using the variable values defined in /usr/lib/smail/config). If the message is for a local machine, the message is handed off to the director.

If the message is for a remote machine, the message's address is given to router drivers to determine to which host the message should be forwarded. The router drivers are specified in the routers file (usually /usr/lib/smail/routers). The file contains the names of the router drivers, each of which (in the order presented in the routers file) is given the message destination address to see whether they have information about the specific route required to send the message.

You don't need to specify any other routers than the default configuration in most cases. The default setup uses the following router steps, in order:

+   - Resolution directly by dotted quad IP address using gethostbyaddr library call
- Resolution by symbolic name using gethostbyname library calls
- Resolution using the pathalias database (given in the file /usr/lib/smail/paths— see the following)
- For UUCP addresses, resolution to see whether the destination is a UUCP neighbor
- Routing to a smart host, if one exists, when other methods to resolve the name have failed

These default routings will work for most systems, although you should comment out the UUCP router if your system is not properly configured to handle UUCP (otherwise, you will get tons of error messages). If you do not plan to use UUCP for mail, you should also comment out this router line to simplify the entire smail system.

A couple of other common situations need to be dealt with. If you are connected to the Internet, there is a problem in that smail's router doesn't recognize the MX record format. In order to properly support Internet mail, comment out the default router and enable the BIND router instead. (If your version of Linux doesn't support BIND, you can obtain and link a more recent version from FTP and BBS sites.)

If you are using both SLIP/PPP and UUCP connections, you may encounter problems with smail waiting too long for a connection. To simplify this type of installation, rearrange the order the routers are checked so that the paths file is checked before the resolver router. In many cases, since UUCP is more efficient and faster than SMTP over a SLIP/PPP line, you can disable the resolver-based router entirely.