# 450 PART 3 | Building a Layered Linux Strategy

Conservatively, a gold virtual baseline includes sufficient RAM, CPU, and hard drive space for the maximum requirements of each component virtual machine. In practice, multiple virtual machines can share RAM and CPU. In other words, properly configured systems don't normally use all their allocated RAM and CPU; you can effectively configure multiple virtual machines to overbook RAM and CPU.

However, KVM does have the following limits with respect to virtual hosts and guests:

+   * Virtual host—KVM can manage up to 256 CPU cores and 1 TB of physical RAM.
* Virtual guest—KVM can support virtual machines with up to 16 CPU cores and up to 256 GB of RAM.

In other words, gold baseline virtual hosts may require a large number of CPUs and a lot of RAM. But such requirements do not necessarily apply to local hard drive storage, as the space required for each virtual guest can be configured on remote storage systems including network attached storage (NAS), direct attached storage (DAS), and *storage area network (SAN)* systems.

To understand "overbooking," consider the following example. As you consider 10 virtual guests that require 512 MB of RAM each. Assume the virtual host requests 1 GB of RAM. In the most heavily loaded situation, system would require about 6 GB of RAM.

If the virtual guests are properly configured, however, they'll need the maximum amount of RAM only. So it is possible that the noted configuration would work on a virtual host with only 4 GB of physical RAM. The hypervisor—also referred as the virtual machine monitor—supports sharing of available RAM and CPU resources by multiple operating systems. In the rare cases every virtual machine is at maximum capacity, the virtual host would use configured swap space.

The actual allocation of RAM and other resources to different virtual hosts depends on the service. The behavior of such virtual hosts depends on the demands on that service. The actual allocation of RAM and other resources to different virtual hosts varies widely.

Once configured, it may be helpful to have a redundant virtual host to go in case of hardware failure. After all, if that virtual host is running 10 or more virtual guests, it is a pretty important part of your network.

# A Baseline Virtual Guest

As just noted, virtual machines on KVM systems are not subject to severe limits. Once a gold baseline virtual machine is configured, it is relatively easy to use. The data in virtual guests are contained in a few files in dedicated directories. To use a gold baseline guest, all you need to do is make a copy of the applicable directory. If virtual guest has been configured with static networking, and other unique information so it doesn't conflict with other virtual guests. But that's it. All you need to do is install and configure the desired service, and it's ready to go.

One question is whether it's appropriate to keep several gold baseline virtual guests, as for those that require extra disk space and for desktops. Fortunately, it is fairly easy to adjust the number of CPUs allocated to a virtual guest in major virtual machine systems, KVM.