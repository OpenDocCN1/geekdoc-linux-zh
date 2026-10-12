```
# chkconfig ypserv on
# chkconfig ypsswd on
```

If you want to start the services immediately, you can type the following:

```
# /etc/init.d/ypserv start
# /etc/init.d/ypsswd start
```

The NIS master server should be up and running. If there are any NIS slave servers, you should configure them now.

# # Setting Up Red Hat Linux as an NIS Slave Server

To set up an NIS slave server, you must configure it as you do an NIS master server, but with one exception: Instead of creating the NIS maps, you run the yppinit command so that the NIS maps can be copied from the server. The option that you give to yppinit is the -s master option, where master is replaced by the name of your NIS master server. Here is an example of running yppinit where the NIS master server is named maple:

```
# /usr/lib/yp/yppinit -s maple
```

As long as the NIS slave server is allowed access, the maps should be copied to your computer from the NIS master server. If the NIS master server goes down, this slave computer should be able to handle NIS requests from the network.

At this point, you can return to the section on setting up NIS as a client to make sure that your NIS server is running properly and distributing the maps to its clients.

# # Summary

DHCP and NIS both provide mechanisms for centrally administering computers on your network. DHCP can provide information that helps client computers get up and running quickly on the network. NIS lets you distribute a wide range of configuration information among Linux and UNIX systems.

DHCP is used to provide information about your network to Windows, Linux, Mac, or other client computers on your network. IP addresses can be assigned dynamically, meaning they are distributed from a pool of IP addresses. Or specific addresses can be assigned to clients, based on specific Ethernet hardware addresses.

You can configure Red Hat Linux as an NIS client, an NIS master server, or an NIS slave server. An NIS client can take advantage of shared information from an NIS server. The NIS master server builds the databases of information (called maps) and enables access to those maps from the network. Optional NIS slave servers can be used to maintain copies of the NIS maps, enabling NIS service to continue on the network in the event that the NIS master server goes down.