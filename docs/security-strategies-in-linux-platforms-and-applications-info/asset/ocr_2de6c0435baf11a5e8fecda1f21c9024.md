# CHAPTER 15 | Best Practices and Emerging Technologies

If the system in question is running a service on which users depend, they'll be thankful when you have a replacement ready to go.

Having a redundant system available depends on the status of the gold baseline. How a gold baseline is maintained depends on its role. The steps required to configure redundant physical systems differ from those needed to maintain redundant virtual systems. For mission-critical services, it may also be helpful to have service-specific baseline systems available.

# A Gold Physical Baseline

Virtualization has in some ways revolutionized the concept of a gold baseline. Before virtualization, gold baselines in computers meant stacks of hard drives, or at least hard drive images ready to be written to other physical devices. But not all systems should be virtualized. Gold physical baselines are important too.

For example, some administrators believe that the demands of database servers make them poor candidates for virtualization. Other administrators have similar beliefs with respect to collation suites such as NovelWise and Microsoft Exchange. Multiple virtual guests on a single virtual host do have latency with respect to Central Processing Unit (CPU) response; in other words, they're slower. The amount of latency, however, is highly debatable. So at least in the future, some virtualization-friendly enterprises will continue to use physical systems for dedicated services.

To end, a gold physical baseline can still be stored as a virtual image. With the dd command, administrators can create image files from the hard drives of their choice. When new copies of the baseline are required, the dd command can also be used to duplicate that image to a new physical device. For example, the following command writes the noted golden.img file

```
# dd if=golden.img of=/dev/sdb
```

# A Gold Virtual Baseline Host

If you're taking advantage of virtual machines, gold baseline systems fall into two categories: virtual hosts and virtual guests. Virtual hosts are physical systems, typically configured with multiple and/or-core CPUs. Multiple virtual guests can run on each virtual host. Each virtual machine system is a guest. To understand the requirements for a gold baseline virtual host, you need to get into the hardware requirements for different virtual guests.

# Hardware Requirements for a Gold Virtual Host

The following is a brief overview of how you can measure the hardware requirements for the virtual host and all virtual guests on that host. This section addresses the basic requirements. For detail, refer to the documentation for the virtualization technology of your choice. Some of these options were briefly discussed in Chapter 2. As noted in previous chapters, major Linux distributions are moving toward the Kernel-based Virtual Machine (KVM) system.