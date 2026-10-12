# Appendix C: Running Network Services

**NOTE:** Some Fedora Linux configuration tools also store configuration information in the `/etc/sysconfig` directory. For example, there are configuration files for `iptables` and sendmail in `/etc/sysconfig`. If you search the scripts in the `/etc/init.d` directory for the word `sysconfig`, you will see just how many services look in that directory for configuration information.

# The xinetd super-server

The `xinetd` daemon is referred to as the *super-server*. It listens for incoming requests for services based on information in separate files in the `/etc/xinetd.d` directory. When a request for a service is received by the `xinetd` daemon (for a particular network port number), `xinetd` typically launches a different daemon to handle the request. So instead of having separate daemons running for every network service, only the `xinetd` daemon needs to run — plus an additional daemon process for each service currently in use.

To see if a particular service handled by `xinetd` is on or off, go to the `/etc/xinetd.d` directory and open the file representing that service with a text editor. A `default` line at the top of the file indicates whether or not the service is on or off by default. The `disable` line actually sets whether or not the service is currently disabled. The following example is an excerpt from the `/etc/xinetd.d/tftp` file:

```
service tftp
{
  socket_type     = dgram
  protocol        = udp
  wait            = yes
  user            = root
  server          = /usr/sbin/in.tftpd
  server_args     = -s /tftpboot
  disable         = yes
  per_source      = 11
  cps             = 100 2
  flags           = IPv4
}
```

In this example, the `tftp` configuration file represents the Trivial File Transfer Protocol (TFTP) service. By default, the service is turned off. When the service is on, a request to the `xinetd` server daemon for a tftp service from the network is handed to the `/usr/sbin/in.tftpd` daemon. The `in.tftpd` daemon, in turn, handles the remote user’s request for file transfer service from this Linux system that is acting as a TFTP server. Other entries in this file contain options that are linked to the TFTP daemon.

To enable a service in an `/etc/xinetd.d` file, edit the file using any text editor as the root user. Turning on the service is as easy as changing the `disable` option from `yes` to `no` and restarting the `xinetd` daemon. For example, you could change the line in the `/etc/xinetd.d/tftp` so that it appears as follows:

```
disable = no
```