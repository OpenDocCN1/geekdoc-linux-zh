# Routers and Bridges

Routers and bridges are used to connect different networks to your network and to connect different subnets within your network. Routers and bridges both serve the same purpose of connecting networks and subnets, but they do so with different techniques. The information in the following sections will help you choose the connection method that best serves your needs.

# Bridges

Bridges are used within a network to connect different subnets. A bridge will blindly relay all information from one subnet to another without any filtering and is often referred to as a dumb gateway. This can be helpful if one subnet in your network is becoming overloaded and you need to lighten the load. A bridge isn't all that good for connecting to the Internet, however, because it lacks filtering. You really don't want all traffic traveling the Internet to be able through your network.

# Routers

Routers can pass data from one network to another, and they allow for filtering of data. Routers are best suited to connect your network to an outside network, such as the Internet. If you have a Web server for an internal intranet that you don't want people to access from the Internet, for example, you can use a router's filter to block port 80 from your network. These filters can be used to block specific hosts from accessing the Internet as well. For these reasons, routers are also called smart gateways.

Routers range in complexity and price from a Cisco brand router that can cost thousands of dollars to other brands that can be less than two hundred dollars.

# Initializing New Network Hardware

All the network configuration and hardware initialization for Red Hat Linux is normally done during installation. There are times, however, when you will need to reconfigure networking on your system, such as when a host needs to be moved to a different subnet or a different network, or if you replace any of your computer's networking.

Linux creates interfaces in memory when the kernel recognizes a NIC or other network device is attached to the system. These interfaces are unlike other Linux interfaces, as serial communications ports, and will not have a corresponding device file in the /dev directory. Unless for a particular NIC is built into your kernel, Linux must be loaded to load a kernel module to support your NIC. More than 100 modules are located in the /lib/modules/2.4.XX-XX/kernel/drivers/net directory

There are several ways to initialize a NIC using Linux. When you first install Red Hat, automatic hardware probing detects and configures your system to any installed NICs. If you remove the original NIC and replace it with a different make and model,