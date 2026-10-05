# Chapter 8 Storage

that a single SAS backplane can accommodate drives of every type. At the logical layer, SATA commands are simply tunneled over the SAS bus.

This convergence is an amazing technical feat, but the economic argument for it is less clear. The expense of a SAS installation is mostly in the host adapter, backplane, and infrastructure: the SAS drives themselves are outrageously priced. Once you've invested in a SAS setup, you may stick as well with SAS from end to end. (On the other hand, perhaps the most modest price for SAS drives are a result of the fact that SAS drives can easily be substituted for them.)

# 8.4 PEELING THE ONION: THE SOFTWARE SIDE OF STORAGE

If you're used to plugging in a disk and having your Windows system ask if you want to format it, you may be a bit taken by the apparent complexity of storage management on UNIX and Linux systems. Why is it so complicated?

To begin with, much of the complexity is optional. Some systems, you can log in your system's desktop, connect that same USB drive, and have much the same experience as on Windows. You'll get a simple setup for personal data storage. If that's all you need, you're good to go.

As usual in this book, we're primarily interested in enterprise-class storage systems: systems that are accessed by many users (both local and remote) that are reliable, high-performance, easy to back up, and easy to adapt to future needs. These systems require a bit more thought, and UNIX and Linux give you plenty to think about.

Exhibit B shows a typical set of software components that can mediate between a raw storage device and its end users. The specific architecture in Exhibit B is for Linux, but our other examples include similar features, although not necessarily in the same packages.

The arrows in Exhibit B mean "can be built on." For example, a Linux filesystem can be built on top of a partition, a RAID array, or a logical volume. It's up to the administrator to construct a stack of modules that connect each storage device to its final application.

Sharp-eyed readers will note that the graph has a cycle, but real-world configurations do not loop. Linux allows RAID and logical volumes to be stacked in either order, but neither component should be used more than once (though it is technically possible to do this).

Here's what the pieces in Exhibit B represent:

+   - A storage device is anything that looks like a disk. It can be a hard disk, a flash drive, an SSD, an external RAID array implemented in hardware, or even a network service that provides block-level access to a remote device. The exact hardware doesn't matter, as long as the device allows random access, handles block I/O, and is represented by a device file.