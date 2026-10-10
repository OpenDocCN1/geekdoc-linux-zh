# ## High-Speed Interconnects

High-speed interconnecting technologies such as InfiniBand, RapidIO, Hyper-Transport, and 10 Gigabit Ethernet are not common in the PC or low-end embedded environments. You are more likely to find them on clusters, blade servers, gaming systems, switches, or high-speed routers. Networking technologies such as Fibre Channel and *Internet SCSI* (iSCSI) can be found in enterprise environments served by *storage-area networks* (SANs).

Let’s peek at the driver subsystems for some of these technologies.

# ### InfiniBand

InfiniBand is a high-speed serial bus standard originally intended to replace PCI. PCI Express, however, has become the accepted future of system buses. Today, InfiniBand technology is commonly used in blade server designs to provide a high-performance storage and networking fabric. InfiniBand supports *Remote DMA* (RDMA), which allows data to be DMA-ed from the memory of one computer system to another.

The Linux InfiniBand subsystem includes core support for InfiniBand, device drivers for host channel adapters, and an implementation of IP over InfiniBand. Look inside *drivers/infiniband/*for the Linux InfiniBand subsystem and at *Documentation/infiniband/*`*` for related documentation.

# ### RapidIO

RapidIO is another high-speed serial bus technology, which is used for connecting boards via a back plane. It supports speeds of the order of 10Gbps. An example processor that supports RapidIO is the power-based MPC8540 from Freescale, targeted at embedded devices such as network routers and switches.

The Linux RapidIO subsystem provides a core set of routines that can be used to drive devices on the RapidIO bus. There are two ways to communicate over a -RapidIO interconnect:

+   1. **Short, out-of-band messages using *doorbells*.** Doorbell services provided by the RapidIO core are `rio_request_inb_dbell()`, `rio_release_inb_dbell()`, `rio_request_outb_dbell()`, **and** `rio_release_outb_dbell()`.

+   2. **High-bandwidth data delivery using *mailboxes*.** Mailbox services provided by the RapidIO core are `rio_request_inb_mbox()`, `rio_release_inb_mbox()`, `rio_request_outb_mbox()`, **and** `rio_release_outb_mbox()`.

Take a look inside *drivers/rapidio/*`*` for the sources.

# ### Fibre Channel

*Fibre Channel* is a modern high-speed serial bus protocol used to talk with storage systems. Fibre Channel interface cards have fiber-optic ports to talk to storage devices on SANs. Fibre Channel is compatible with SCSI, so a Fibre Channel device driver is essentially a SCSI driver with extras to handle fiber channels.

Linux supports a Fibre Channel core and device drivers to handle Fibre Channel hardware. Look inside *drivers/fc4/*`*` for the sources.