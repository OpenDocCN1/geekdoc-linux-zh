# Extended Internet Services Daemon (xinetd)

If your system averages only a few requests for a specific service, you don't need the server for that service running all the time. You need it only when a remote user is accessing its service. The Extended Internet Services Daemon (xinetd) manages Internet servers, invoking them only when your system receives a request for their services. xinetd checks continuously for any requests by remote users for a particular Internet service; when it receives a request, it then starts the appropriate server daemon.

The xinetd program is designed to be a replacement for inetd, providing security enhancements, logging support, and even user notifications. For example, with xinetd you can send banner notices to users when they are not allowed to access a service, telling them why. xinetd security capabilities can be used to prevent denial-of-service attacks, limiting remote hosts' simultaneous connections or restricting the rate of incoming connections. xinetd also incorporates TCP, providing TCP security without the need to invoke the tcpd daemon. Furthermore, you do not have to have a service listed in the /etc/services file. xinetd can be set up to start any kind of special-purpose server. The Red Hat Linux versions 7.0 and up use xinetd.

# Starting and Stopping xinetd Services

You can start, stop, and restart xinetd using its startup script in the /etc/rc.d/init.d directory, as shown here:

```
# service xinetd stop
# service xinetd start
# service xinetd restart
```

On Red Hat, you can also turn on and off particular xinetd services with chkconfig, as described earlier. Use the on and off options to enable or disable a service. chkconfig will edit the disable option for the service, changing its value to "yes" for off and "no" for on. For example, to enable the swat server, you could enter:

```
chkconfig swat on
```

# xinetd Configuration: xinetd.conf

The xinetd.conf file is the configuration file for xinetd. Entries in it define different servers to be activated when requested along with any options and security precautions. An entry consists of a block of attributes defined for different features, such as the name of the server program, the protocol used, and security restrictions. Each block for an Internet service such as a server is preceded by the keyword service and the name by which you want to identify the service. A pair of braces encloses the block of attributes. Each attribute entry begins with the attribute name, followed by an assignment operator, such as =, and then the value or values assigned. A special block specified by the keyword default contains default attributes for services. The syntax is shown here:

```
service <service_name>
{
<attribute> <assign_op> <value> <value> ...
...
}
```

# xinetd Attributes

Most attributes take a single value for which you use the standard assignment operator, =. Some attributes can take a list of values. You can assign values with the = operator, but you can also add or remove items from these lists with the += and -= operators. Use += to add values and -= to remove values. You often use the += and -= operators to add values to attributes that may have an initial value assigned in the default block.