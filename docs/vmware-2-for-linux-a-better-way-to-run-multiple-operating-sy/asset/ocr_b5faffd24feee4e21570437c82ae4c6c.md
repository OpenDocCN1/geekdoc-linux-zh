Is Samba better than using FTP? Maybe. Try both and decide. Then use NFS, and you'll probably never look back.

# File Sharing with NFS

NFS, the Network File System, is one of the oldest and most well-established file-sharing systems in the UNIX world. It provides a powerful alternative to FTP, Samba, and virtual disk mounting. Although somewhat more difficult to configure, it is arguably the best way to share files between a Linux host and Linux (or other UNIX-family) guest.

> These examples presume that you are using bridged networking, but the principles are the same for host-only networking. Unlike the VMware-specific Samba server, the generic implementation of NFS you will be using does not care how network requests are received.

# Using NFS with a Linux Guest

Many Linux distributions come with most of the necessary components for NFS server operation already installed and running. If in doubt, you might want to use your installation's package manager to add NFS components to your host system before you proceed. Alternately, you can search for Linux NFS packages through services such as http://www.rpmfind.net.

> The principles in this section apply equally well to a FreeBSD guest, along with any other UNIX-style operating systems you might be able to run someday in VMware.

> Read the NFS HOWTO at http://www.linuxdoc.org/HOWTO/NFS-HOWTO.html.

A basic understanding of NFS will help you make sense of the steps necessary to enable NFS between the host and guest.