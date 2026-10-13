# Network Installation

You can install Linux through three different types of networks: File Transfer Protocol (FTP), Network File System (NFS), or Samba. FTP is a common way to transfer files to and from other networks, such as the Internet. NFS is the standard Linux network file sharing protocol. Samba is a heterogeneous protocol that allows Linux computers to exchange files with Microsoft and IBM operating systems.

Whichever network you use, the first step is to find Linux boot disks that allow you to connect to a network server. These special boot disks usually detect your network card. However, if these disks don't detect your card, you may need to add information like the Linux name for your network driver, its interrupt request (IRQ) and input/output (I/O) channels, and memory addresses.

> *Note: Most commands in Linux are lowercase. For example, if you're installing a Novell-compatible network card that's set to IRQ 10 with an I/O address of 0x300, you might use the `insmod ne i/o=300 irq=10` command to help Linux recognize your card.*

Once you've booted your computer, you'll need the host and domain names or IP address for the remote server. You also need to know the remote directory where the installation files are stored.

When installing Linux over a network, the devil is in the details. If you get "little" things wrong, such as the case of a password or a missing slash in your directory, they can prevent a successful installation.

Don't try installing Linux over a telephone modem. If everything goes perfectly, installation takes several days. If you have any "normal" problem with a modem connection, the process may take quite a bit longer.

# Seven Major Distributions

As of this writing, there are perhaps two dozen Linux distributions. Fortunately, they all run the same kind of software. Because of the General Public License (GPL), there are few copyright limitations on what is packaged. Some distributions even repackage identical versions of others, perhaps with a few additional tools. They all share the same basic Linux kernel.

Each distribution comes with a version number. Generally, they follow the same model as Red Hat 7, where the first number signifies a major change, and the second number indicates a relatively small revision.