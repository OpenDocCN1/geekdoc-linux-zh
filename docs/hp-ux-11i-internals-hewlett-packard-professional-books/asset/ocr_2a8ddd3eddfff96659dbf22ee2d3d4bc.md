# Chapter 10

# # I/O and Device Management

T he I/O subsystem is one of the most complicated parts of the HP-UX operating system. As each new generation of hardware is developed, it brings along with it new types of busses, new device adapters, and new devices. Over time the kernel has had to change to accommodate these new advances while maintaining compatibility with old hardware. As a result, the I/O subsystem has grown into a large and complex framework that involves many smaller subsystems and a lot of "glue" to hold it all together.

# ## PA-RISC I/O Architecture

The PA-RISC I/O architecture has specific requirements for all PA-RISC systems. These are designed to provide a standard set of rules for how the I/O hardware works and communicates with other components.

Every PA-RISC system must have at a minimum at central bus to which must be attached at least one processor module and at least one memory module. If the system has more than one processor or more than one memory module, they all reside on the central bus.

There are also a number of possible native busses. A native bus is one that adheres to the PA-RISC I/O architecture. As hardware has evolved since the introduction of PA-RISC, a number of new native busses have been introduced. One of the earliest of these was the HP Precision Bus (HP-PB), also called the native I/O (NIO) bus. Some others include the high-speed connect (HSC) bus, Gecko System Connect (GSC) bus, summIt bus, and runway bus. Each provides different capabilities and performance points, but all are native busses.

In addition to the native busses, PA-RISC systems must be able to connect to a variety of busses that were not designed with PA-RISC in mind. These are known as foreign busses. Some examples are Extended Industry Standard Architecture (EISA), Peripher al Component Intercon-