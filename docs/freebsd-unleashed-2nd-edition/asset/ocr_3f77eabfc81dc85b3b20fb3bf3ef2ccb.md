# Selecting an NFS Install

At the Choose Installation Media screen, select NFS. You will then be asked to enter the name of the NFS server followed by the path where the FreeBSD installation files are located. In the example in Figure 3.6, the server is lion and the installation directory is install/FreeBSD.

![](bbox=[0.37, 0.2, 0.68, 0.35])

**FIGURE 3.6** Specifying the NFS location of the remote FreeBSD installation files.

Once you have entered this information, you will need to configure the network (shown previously in Figure 3.5). Follow the procedure shown in Chapter 2 under the “Configuring the Network” heading for instructions on how to do this.

Once you have finished configuring the network, the various distribution sets will be downloaded from the remote server and installed. This will naturally take longer than installing from a CD-ROM, but it will likely be faster than an FTP installation. When files have finished copying, you can go ahead with the “Post-Installation” section of Chapter 2. Because you have already configured the network to do the installation, you can skip the network-configuration portion.

Note that this chapter has covered only how to install FreeBSD from an NFS server. If you want to set up an installation server that can be used by clients to install FreeBSD over NFS, see Chapter 32. Once you have an NFS server set up and the FreeBSD installation files available on it, you can have other systems install from it using the procedures discussed in this chapter.