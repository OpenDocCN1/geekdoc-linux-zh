the configuration utility failed to configure your system properly. You may also wish to do so if your system has an unusual or unique configuration.

# ## Required Information

To configure your computer properly, you should obtain the following information from your network administrator or your Internet service provider:

+   * **Domain name** This is the registered name of the domain to which you are connecting. For example, if you are connecting to an ISP named cstone.net, your domain name is cstone.net. If you are connecting to the University of Virginia's local area network, your domain name is virginia.edu.

+   * **Hostname** The name you should assign to your computer. The name should consist of two parts, separated by a dot. The first part is a unique name that is not taken by any other computer on the network to which you are connecting. The second part is the network *domain name*. An example of a valid domain name is bpmac.seas.virginia.edu.

+   * **IP address** If your computer requires a static IP address, obtain this address; you'll need to supply it to the various configuration files. If you're connecting via a modem to an Internet service provider, chances are that you'll be given a dynamic IP address each time you connect to the ISP's computer.

+   * **Gateway device** If you're connecting to a local area network that uses a gateway device (such as a bridge, router, ISDN router, or some other device), you'll need the device's IP address.

+   * **Search domain and DNS servers** The *search domain* defines the default domain to search for IP addresses. Generally, this is the same as the domain name. You'll probably be given two DNS server addresses, one IP address each for the *primary nameserver* and the *secondary nameserver*.

+   * **Netmask** If you are connecting to a Class C network, the default netmask is 255.255.255.0. The default for Class B networks is 255.255.0.0. On large local area networks that are professionally