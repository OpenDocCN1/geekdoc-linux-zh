
called *northbound* and *southbound*. Other applications on the network see the SDN as a logical network switch.  
Overlay networks offer better flexibility and utilization than nonvirtualized network solutions. They also reduce costs and provide significant scalability.

## Configuring Virtualized NICs

Virtual NICs (adapters) are sometimes directly connected to the host system's physical NIC. Other times they are connected to a virtualized switch, depending on the configuration and the hypervisor used. An example of a VM's adapter using a virtual switch is shown in Figure 29.2.

### FIGURE 29.2 Virtual machine using a virtual switch

![](img/c0a399aca0d18f8822d714ad0a173123_870_0.png)

When configuring a virtual machine's NIC, you have lots of choices. It is critical to understand your options in order to make the correct selections.

- **Host-Only**: A *host-only adapter* (sometimes called a *local adapter*) connects to a virtual network contained within the virtual machine's host system. There is no connection to the external physical (or virtual) network to which the host system is attached.

The result is speed. If the host system has two or more virtual machines, the network speed between the VMs is rather fast. This is because VMs' network traffic does not travel along wires or through the air but instead takes place in the host system's RAM.

This configuration also provides enhanced security. A virtual proxy server is a good example. Typically, a proxy server is located between a local system and the Internet. Any web requests sent to the Internet by the local system are intercepted by the proxy server, which then forwards them. It can cache data to enhance performance, act as a firewall, and provide privacy and security. Any virtual machine on the host can act as a proxy server utilizing a different NIC configuration and have the ability to access the external network. The other virtual machine employing the host-only adapter sends/receives its web requests through the VM proxy server, increasing its protection.

- **Bridged**: A bridged NIC makes the virtual machine like a node on the LAN or VLAN to which the host system is attached. The VM gets its own IP address and can be seen on the network.

In this configuration, the virtual NIC is connected to a host machine's physical NIC. It transmits its own traffic to/from the external physical (or virtual) network.

This configuration is employed in the earlier virtual proxy server example. The proxy server's NIC is configured as a bridged host, so it can reach the external network and operate as a regular system node on the network.

- **NAT**: A network address translation (NAT) adapter configuration operates in a way that's similar to how NAT operates in the physical world. NAT in the physical networking realm uses a network device, such as a router, to “hide” a LAN computer system's IP address when that computer sends traffic out onto another network segment. All the other LAN systems' IP addresses are translated into a single IP address to other network segments. The router tracks each LAN computer's external traffic, so when traffic is sent back to that system, it is routed to the appropriate computer.

With virtualization, the NAT table is maintained by the hypervisor instead of a network device. Also, the IP address of the host system is employed as the single IP address that is sent out onto the external network. Each virtual machine has its own IP address within the host system's virtual network.

Physical and virtual system NAT has the same benefits. One of those is enhanced security by keeping internal IP addresses private from the external network.

- **Dual-Homed**: In the physical world, a dual-homed system (sometimes called a multi-homed system) is a computer that has one or more active network adapters. Often, a physical host is configured with multiple NICs. This configuration provides redundancy. If one physical NIC goes bad, the load is handled by the others. In addition, it provides load balancing of external network traffic.

In the virtual world, many virtual machines are dual-homed or even multihomed, depending on the virtual networking environment configuration and goals. Looking back to our virtual proxy server example, it is dual-homed, with one internal network NIC (host-only) to communicate with the protected virtual machine, and it has a bridged adapter to transmit and receive packets on the external network. Figure 29.3 shows the complete network picture of this virtual proxy server.

### FIGURE 29.3 Virtual proxy server

![](img/c0a399aca0d18f8822d714ad0a173123_872_0.png)

The physical and virtual machine network adapter configuration has performance and security implications. Understanding your internal virtual and external physical networks and goals is an important part of making these choices.

> Most container packages such as Kubernetes and Docker allow you to create a *service mesh* between applications. The service mesh is a dedicated infrastructure layer on top of the network that helps facilitate service-to-service communication. This enables separate parts of an application to communicate with each other in a high-speed manner.

## Summary

Configuring your cloud and/or virtualization environment requires knowledge concerning networking and storage options. In addition, you need to understand how to quickly boot large numbers of virtual machines as well as bootstrap new ones. Discerning some of the various virtual and cloud machine tools is important as well. With a firm grasp on these concepts, you can participate in cloud and virtual system planning teams, which can successfully migrate a company's physical systems to a more modern and cost-effective environment.

## Exam Essentials

- Describe various VM tools. The `libvirt` library is a popular software collection of virtualization management components. It includes an API, a daemon (`libvirtd`), and command-line utilities, such as `virt-install` and `virsh`. The `virsh` shell is one such tool provided by the `libvirt` library that allows you to manage a system's virtual machines. The Virtual Machine Manager (also called VMM) is a lightweight desktop application for creating and managing virtual machines. You can initiate it from the command line by issuing the `virt-manager` command in a terminal emulator.
- Explain bootstrapping utilities. The kickstart installation method employs a kickstart file that contains all the bootstrap choices desired for a new system. Instead of starting from scratch, the `anaconda` file, `/root/anaconda-ks.cfg`, is available on Red Hat-based distros and can be modified to configure a kickstart file. Ubuntu distributions do not employ the kickstart installation method by default. Instead they use a bootstrapping product named `preseed`. openSUSE distros also have their own alternative, which is AutoYaST. The Canonical product, `cloud-init`, is a bootstrap utility that is available for local virtual machines as well as cloud-based ones.
- Detail the various virtual storage options. Virtual disks can be provisioned either thick or thin. Thick provisioning is a static setting where the virtual disk size is selected and the physical file(s) created on the physical disk is preallocated. Thin provisioning is grown dynamically, which causes the hypervisor to consume only the amount of disk space actually used for the virtual drive. Drives can be either persistent or temporary. Temporary volumes are discarded when the virtual machine is stopped, whereas persistent disks are kept not only when the VM is shut down but sometimes even after it is deleted. Blob storage refers to unstructured data offered on the Microsoft Azure cloud platform. This storage typically consists of images, streaming video and audio, big data, and so on. There are three blob types—block, append, and page.
- **Summarize virtual network configurations.** One network type is an overlay network. This network virtualization method uses encapsulation and communication channel bandwidth tunneling. Besides the typical network hardware, this network type employs virtual switches, tunneling protocols, and software-defined networking (SDN). Network adapters (NICs) also have many configuration virtualization options. A dual-homed virtual machine has two virtualized NICs. A host-only adapter connects to a virtual network contained within the virtual machine's host system, and there is no connection to the external network. A bridged NIC makes the virtual machine like a node on the network to which the host system is attached. A NAT adapter creates a virtualized NAT router for the VM.
