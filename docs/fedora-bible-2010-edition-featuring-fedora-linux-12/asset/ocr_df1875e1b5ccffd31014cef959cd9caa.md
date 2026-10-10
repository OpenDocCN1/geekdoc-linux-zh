to run — plus an additional daemon process for each service currently in use. (Install the xinetd package, if you do not have xinetd installed.)

To see if a particular service handled by xinetd is on or off, go to the /etc/xinetd.d directory and open the file representing that service with a text editor. The disable line sets whether or not the service is currently disabled. The following example is an excerpt from the /etc/xinetd.d/amanda file:

```
```
service amanda
{
    socket_type    = dgram
    protocol       = udp
    wait           = yes
    user           = amanda
    server         = /usr/lib/amanda/amandad
    server_args    = -auth=bsd amdump
    disable        = yes
}
```
```

In this example, the amanda configuration file represents a means of retrieving backup index files from amanda clients. By default, the service is turned off. When the service is on, a request to the xinetd server daemon for the amandad service from the network is handed to the amandad daemon. Arguments to that daemon are set on the server_args line.

To enable a service in an /etc/xinetd.d file, edit the file using any text editor as the root user. Turning on the service is as easy as changing the disable option from yes to no and restarting the xinetd daemon. For example, you could change the line in the /etc/xinetd.d/amanda file so that it appears as follows:

```
```
disable    = no
```
```

Then you could restart the xinetd daemon by typing the following:

```
```
# service xinetd restart
```
```

> **NOTE:** Although not all services support this, the xinetd service lets you use the reload instead of the restart option with the service command just shown. With xinetd already running, a reload can occur faster and with less interruption to system services by not completely shutting down xinetd.

> **CROSS-REFERENCE:** The xinetd super-server is described in Chapter 13.

# The init.d startup scripts

Most network services are not available via the xinetd daemon, but rather by scripts in the /etc/init.d directory. For a script in the /etc/init.d directory to activate a service, it