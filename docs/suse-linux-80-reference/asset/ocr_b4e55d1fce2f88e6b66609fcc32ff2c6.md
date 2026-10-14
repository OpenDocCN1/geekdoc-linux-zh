# Defining a Suitable Printer Driver

In the lists mentioned in Section *Hardware and Software Requirements* on the page before, Ghostscript drivers for specific printer models are provided. If your supplier cannot give any Linux-specific information on your printer model, the following tips may help:

+   - Find out if your printer is compatible with a model that does run in Linux then use the Ghostscript driver for this compatible model. “Compatible in Linux” means that your printer can print correctly with the same binary control sequences as the compatible model — the printer can “understand” the same printer language directly (rather than just being capable of emulating it in Windows through the driver software).

The fact that two printers have similar names is not always a guarantee that they are compatible. This is because printers with similar names do not always understand the same printer language directly.

+   - The best source of information about your printer’s native language is the manufacturer. In many cases, find the printer language listed among the technical data in the printer manual. Some examples of existing printer languages are given in Section *Examples of Default Printer Languages* on page 192.

# Connecting Printers Locally

# Parallel Ports

A printer can be connected to a Linux system via a parallel port. A printer on a parallel port is addressed by the kernel’s parport subsystem. The basic configuration of a parallel port with YaST2 is explained in the *Basics* manual in Section *Manual Configuration*, so only supplemental information is provided here. The parallel port must be made known to the parport subsystem by loading architecture-specific kernel modules. In this way, a number of devices in series can be used simultaneously via one parallel port. The numbering of the device files for parallel port printers begins with `/dev/lp0`. To print over the first parallel port, the modules `parport`, `parport_pc`, and `lp` must be loaded for a SuSE standard kernel. This is normally taken care of by the Kernel Module Loader, kmod (see Section *Kmod — the Kernel Module Loader* on page 232) as soon as the corresponding device file (e.g., `/dev/lp0`) is accessed.