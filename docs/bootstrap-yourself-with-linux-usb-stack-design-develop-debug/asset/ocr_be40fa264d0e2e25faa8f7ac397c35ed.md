# USB: The Path and the Market

# Note

**Low speed.** Devices that do not transfer large amount of data fall into this category. These include interactive devices such as keyboards and joysticks. The typical transfer rate for these devices is 10–100kbps.

**Full speed.** Applications such as microphones and broadband fall into this category, which requires a transfer rate of 500kbps–10Mbps. One of the important attributes is guaranteed bandwidth and latency.

**High speed.** High-bandwidth devices such as imaging and storage that require higher and sometimes guaranteed bandwidth fall into this category. A typical transfer rate is 25–400Mbps.

The year 2001 introduced a new generation of device supplement that provides a minimal host facility, enabling the devices to act as host and connect to other USB devices. These are called On-the-Go (OTG) devices. OTG mainly evolved to support handheld devices such as mobile phones directly connecting to other USB devices as printers.

The USB specification has a complex low-level protocol implementation with strict timing requirements. Most of the complexity is implemented as hardware. Although this book concentrates on the software aspect of USB, it is important to know the different hardware configurations available in the market. This information helps you when you write drivers for these controllers. The following section captures in broad terms various USB hardware configurations available in the market.

# USB Hardware

A USB system implements the most complicated portion of the USB specification as part of USB hardware, which includes a physical layer, a link layer, and some part of the USB protocol. The physical portion characteristics that are necessary for data transmission, speed detection, timing, and power. The hardware protocol management includes bandwidth management, error handling, and packet management.

In the market, you may find USB hardware in different configurations and casings, providing flexibility to a platform when adopting a USB solution. USB solutions extend the functionality of a platform in a shorter time to integrate,