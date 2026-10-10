Linux core, but may not be started. Once it is installed, start it by typing `service vncserver start`. If you are starting the server for the first time, you must type in a password at the prompt twice, which will be used by the remote client. The server is now started and ready to accept connection from a remote client.

There are a number of VNC clients available, and the one you use will depend on the company policy, the ease of use, and the level of security you wish to have. VNC operates on port 5901, and hence this needs to be opened up in any intermediate firewall [and possibly on your host firewall, if you have one]. A client for X Windows will be `vncviewer`, which will connect to any VNC-compatible server.

# Samba

Samba will implement the basic CIFS services, namely

+   - File and print services
+   - Authentication and authorization
+   - Name resolution
+   - Browsing or service announcement

Most end users will be interested in the file and print services; that is, the capability to share files between computers and to share printers. As with any system, a user may wish to share some of all their files and only allow certain users access (authentication and authorization). All of these are handled by the `smbd` daemon that is included within Samba.

The other daemon included with Samba is `nmbd`, which is basically name resolution on a point-to-point or broadcast basis. This daemon essentially is using the NetBIOS protocol to undertake the tasks. In broadcast mode, a client will send out a request to all machines on the network; for example, asking who is running a particular service. This may cause a lot of network traffic; but as it is confined to the local LAN, it is not usually an issue.

The other name resolution element of the `nmbd` daemon revolves around the NetBIOS Name Service (NBNS), or Microsoft's implementation of this, called Windows Internet Name Service (WINS). Within NBNS, there is a master NBNS server, which holds the IP address and NetBIOS name of each client or server on the network. The NBNS server will act like a normal nameserver; and when a client sends a request to it about a particular client name, the NBNS server will return an IP address if it is in its database.

The browsing or service announcement part of Samba is also handled by the `nmbd` daemon. This should not be confused with Web browsing, but