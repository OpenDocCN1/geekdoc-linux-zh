# A.8 Low power

For the most part, TinyOS will automatically put systems and hardware into the lowest power state possible. For peripherals, this typically works through power locks (Section 11.2). For example, when an application writes or reads from a flash chip, TinyOS will automatically power it on, perform the operation, then power it down when done.

Communication is the major exception to this behavior. Because communication subsystems, such as the radio and serial port, need to be able to receive as well as transmit, TinyOS needs an application to explicitly tell it when it can safely turn them on and off via SplitControl interfaces.

In the case of the radio, however, there are many techniques one can use to save power. For example, rather than always keep the radio on, TinyOS can keep it off most of the time, periodically turning it on just long enough to hear if there’s a packet. A transmitter sends a packet multiple times, until the receiver wakes up, hears it, and acknowledges it, or a timeout occurs.

A complete discussion of how to set these intervals is beyond the scope of the book. The important interface is LowPowerListening, which some (but not all) radios provide. LowPowerListening allows an application to set a radio’s check interval and also the check interval it expects of a receiver. TinyOS has a tutorial for how to use this interface when writing a low-power application, and Section 12.2.3 has a brief example of its use.