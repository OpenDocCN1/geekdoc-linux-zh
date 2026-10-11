+   ➤ net.slp.MulticastRadius—This parameter specifies the time to live (TTL) value for the SA multicast packets. The default value is 32.

+   ➤ net.slp.useScopes—This parameter specifies a list of scopes that the local SA is allowed to use when registering or querying for services.

+   ➤ DA_ADDR—This parameter is used to statically configure the local SA with the IP address of the DA or DAs it is to register its services with.

> TIP
> Recall earlier that I said SAs, by default, send out a DA discover multicast message when they are started. If they find a DA, they register their services with it. If not, they default to SA-Only mode. If you list an IP address for the DA_ADDR parameter, however, the SA will not do this. Instead, it will contact the specified DAs and register its services with them only.
> This is a very useful parameter if your network routers aren't configured to forward multicast traffic. By you specifying a DA in this parameter, your SA will contact it using unicast transmissions.
> The syntax is as follows:
> `DA_ADDR = DA_IP_address, scope_name`
> Once you have configured your slpusera.conf file, you next need to restart the slpusera daemon. This is done using the slpusera script located in /etc/init.d.

> TIP
> On other distributions, such as Red Hat, the script is located in /etc/rc.d/init.d.

To stop the daemon, open a terminal session and enter `/etc/init.d/slpusera stop`. To start the daemon, open a terminal session and enter `/etc/init.d/slpusera start`. Because SLP is so critical to the operation of eDirectory and other NNLS components, you should use the `chkconfig` command to make the service start automatically each time the system starts. To do this, enter `chkconfig slpusera 345` at the shell prompt.

# Configuring OpenSLP

As discussed earlier, Novell actually recommends that you don't use the slpusera daemon on any implementation where there are more than a handful of servers or where the eDirectory tree has many partitions and replicas. If you want to implement a DA on a Linux server, this is even more applicable because the slpusera daemon doesn't include DA functionality.

> WARNING
> Novell's SLP implementations on NetWare and Windows do include DA functionality. Many administrators are tempted to implement a DA on one of these platforms