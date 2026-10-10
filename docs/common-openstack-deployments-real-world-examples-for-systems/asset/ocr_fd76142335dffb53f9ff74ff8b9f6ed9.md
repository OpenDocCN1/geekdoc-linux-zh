# # Virtual Machines

Using virtual machines for these deployment examples will likely be significantly easier as you start out. In the reference deployment in Appendix A, we're using a virtualized environment powered by KVM running on Ubuntu 14.04. If you understand the architecture we're aiming for, you're welcome to use an alternate virtualization technology that you're comfortable with.

# ## Host, Node and Instance

It's easy to get confused when we start talking about the components of an environment where you have a single physical machine with a whole bunch of virtualization on top. The following will define what we mean when we use each term.

+   * **Host:** This is the hardware where all your virtual machines will run. It can be a laptop, a desktop or a server, but it should be something you can sit in front of and run commands on. This host will need to run some form of Linux and you will be setting up Linux Bridges on it for use by the nodes.
+   * **Node:** A node is a component of OpenStack that runs OpenStack services. In our examples you'll have a controller node and a compute node. Other OpenStack deployments may have their own network nodes, storage nodes and more. This would normally be its own physical machine.
+   * **Instance:** This is the server you use OpenStack to launch and on which you do all your organization's work. It'll be where you host your web site or the server for the latest game your company you released. It will typically be a virtual machine, but may also be bare metal as we will discuss in Chapter 10, “Bare Metal Provisioning,” or a container, which is covered in Chapter 11, “Containerizing Containers.”

The virtual machine setup will be identical to the physical machine setup, but you will be replicating the scenario virtually. Instead of switches you will be using bridges on the host for each node, so the machine hosting them will need to be configured with two bridges. Other than that, Figure 3.3 should look very similar to Figure 3.2, and comparing the two may help you conceptualize the configuration.

When you create your controller node, one NIC should be associated with virbr0 and the second NIC with virbr1. The NIC connected to the virbr0 network will be how you access the system to configure and interact with OpenStack. Management traffic on this bridge will need access to the Internet through osh (shown in dotted lines in Figure 3.3), or installs NAT rules put typically be put in place to allow for this.

The second bridge (virbr1) will be used for the example external provider network, which is meant to give your instances access beyond their default tenant networks. Your single NIC compute node must only be associated with the virbr0 bridge.