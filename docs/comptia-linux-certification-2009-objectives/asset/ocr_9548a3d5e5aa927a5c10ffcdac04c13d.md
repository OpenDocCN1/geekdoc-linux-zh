**Example:**

![](bbox=[0.24, 0.1, 0.52, 0.42])

*Figure 12-46: The working of the portmapper program.*

# # The portmap Daemon

**Definition:**

*The portmap* service is a daemon that dynamically assigns ports to RPCs for communication between clients and servers. It maps a service name to the port number in which the service is running. It maintains a portmapper that contains a list of ports and the services that are available for access at each port. The portmap program is stored in the /sbin directory. The portmap service can be started only by a superuser.

![](bbox=[0.75, 0.49, 0.83, 0.54])

The portmap Daemon