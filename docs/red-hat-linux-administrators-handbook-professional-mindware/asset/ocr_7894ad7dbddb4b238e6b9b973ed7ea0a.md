If you have more than 1GB of physical RAM, you need to select y here.
If you have not used the 2GB memory model, use the default-value.

Networking support (CONFIG_NET) [Y/n/?]

This is a dumb question, isn’t it? Who wants to run Linux and not have networking support? Perhaps there are a few out there. The default is a must.

PCI support (CONFIG_PCI) [Y/n/?]

Unless you are on a really old x86 system that has only an ISA bus, the default is fine. Note that on SPARC systems you might not need PCI support if you have only sbus cards.

PCI access mode (BIOS, Direct, Any) [Any]

The default option allows the kernel to detect the PCI configuration by using the direct method; if that fails, it gets PCI configuration from the system BIOS, so the default is fine.

PCI quirks (CONFIG_PCI_QUIRKS) [Y/n/?]

This option is for motherboards with lousy BIOSes that fail to set up the PCI bus properly. If you don’t have such a board, select n for no. If you are unsure, keep the default.

MCA support (CONFIG_MCA) [N/y/?]

Unless you have an IBM PS/2 Micro Channel Architecture (MCA)–based system, you do not need MCA support.

SGI Visual Workstation support (CONFIG_VISWS) [N/y/?]

If you are not using an SGI system, keep the defaults.

System V IPC (CONFIG_SYSVIPC) [Y/n/?]

Many programs need Inter Process Communication (IPC); therefore, the default is a must.

BSD Process Accounting (CONFIG_BSD_PROCESS_ACCT) [N/y/?]