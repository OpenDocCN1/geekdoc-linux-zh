# **Polling Hypervisors**

The agent used for polling the hypervisor needs pretty significant view into what these systems are doing. This means it also needs support for how these hypervisors are being queried. In Mitaka, the following hypervisors are supported:

+   - KVM and QEMU, used in our reference deployment (via libvirt)
+   - LXC (via libvirt)
+   - UML (via libvirt)
+   - Hyper-V
+   - Xen
+   - VMware vSphere

There is also an intelligent Platform Management Interface (IPMI) agent for queries against bare metal. We have specifically excluded support for IPMI in our deployment scenarios because we aren’t supporting it.

# **Viewing Statistics: Dashboard**

The Horizon dashboard support for Ceilometer is limited and will likely be considerably different in the future. For now, a quick view into the display of statistics can be seen by logging in as the admin user and navigating to the Admin, System, Resource Usage.

The first screen will give you a listing of some of the meters and data they have collected, as shown in Figure 7.3.

![](bbox=[0.1, 0.58, 0.9, 0.95])