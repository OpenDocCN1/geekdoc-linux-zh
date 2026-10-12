# TABLE 38.1 Continued

| Name | Description |
| --- | --- |
| Networking support | Several options for the configuration of networking in the kernel. The options are for the types of supported protocols and configurable options of those protocols. |
| Amateur radio support | Options for configuring support of devices that support the AX25 protocol. |
| IrDA (infrared) support | Options for configuring support of the infrared Data Association suite of protocols and devices that use these protocols. |
| Bluetooth support | Support for the Bluetooth wireless protocol. Includes options to support the Bluetooth protocols and hardware devices. |
| ISDN subsystem | Options to support Integrated Services Digital Networks protocols and devices. ISDN is a method of connection to a large area network digitally over conditioned telephone lines, largely found to connect users to ISPs. |
| Telephony support | Support for devices that enable the use of regular telephone lines to support VOIP applications. This section does not handle the configuration of modems. |
| Input device support | Options for configuring Universal Serial Bus (USB) Human Interface Devices (HID). These include keyboards, mice, and joysticks. |
| Character devices | Configuration options for devices that communicate to the server in sequential characters. This is a large subsection containing the drivers for several motherboard chipsets. |
| Multimedia devices | Drivers for hardware implementations of video and sound devices such as video capture boards, TV cards, and AM/FM radio adapter cards. |
| Graphics support | Configures VGA text console, video mode selection, and support for frame buffer cards. |
| Sound | Large subsection to configure supported sound card drivers and chipset support for the kernel. |
| USB support | Universal Serial Bus configuration options. Includes configuration for USB devices, as well as vendor-specific versions of USB. |
| File system | Configuration options for supported file system types. See Chapter 37 for a description of the file systems supported by the kernel. |
| Additional device driver support | A section for third-party patches. |
| Profiling support | Profiling kernel behavior to aid in debugging and development. |
| Kernel hacking | This section determines whether the kernel will contain advanced debugging options. Most users will not want to include this option in their production kernels because it increases the kernel size and slows performance by adding extra routines. |
| Security options | Determines whether NSA Security Enhanced Linux (SELinux) is enabled. |
| Cryptographic options | Support for cryptography hardware (Fedora patches not found in the “vanilla” kernel sources). |
| Library routines | Contains zlib compression support. |