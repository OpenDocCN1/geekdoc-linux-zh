![](bbox=[0.29, 0.1, 0.73, 0.22])

Figure 4.1 Minimum requirements for the simple, two node deployment

If you're using VMs for this setup, adding a second NIC should be simple. See the documentation for your VM technology for how to do this. As in Chapter 2, for best performance you also will need to use a 64-bit CPU with hardware virtualization support and, preferably, at least four cores, so you can launch an instance.

# ## Reference Deployment

The examples in this book are intended to be flexible enough to work with your choice of virtualization technology or hardware setup. However, if you are satisfied with using a deployment example prepared and tested by the authors, see Appendix A, “Reference Deployment.” This reference deployment walks you through using an Ubuntu 14.04 system as a host with Linux Bridges, the libvirt toolkit with KVM (Kernel-based Virtual Machine) for the OpenStack nodes and QEMU for compute instances.

Use of the reference deployment is also recommended if you’re struggling to get the configurations working on your own choice of setup. Nuances regarding networking defaults, in particular, vary between virtualization technologies and can easily put you in a situation that is difficult to debug while you’re also learning OpenStack fundamentals.

# ## Initial Setup

You will begin by satisfying the prerequisites needed for a working network. Once your network is set up, we’ll then complete an installation of the operating system on your system and install the key components of OpenStack. As discussed in Chapter 1, “What is OpenStack?” the operating system we’ll be using is Ubuntu 14.04 LTS Server, and we’ll be installing the Mitaka release of OpenStack. This chapter leads you through creating a fully manual network to get you familiar with the specific components. In the next chapter you’ll be introduced to how we do this with Puppet.

# ## Networking

In Chapter 3 you learned about the internals of how networking works in OpenStack and, specifically, how it works for the deployments we’re working on. If you’re using a physical network set up according to Figure 3.2 in Chapter 3, the virtualized networking we’ll be talking about in this section is instead handled by the hardware on your network. With your physical network in place, you can skip to the next section, “Operating System.”