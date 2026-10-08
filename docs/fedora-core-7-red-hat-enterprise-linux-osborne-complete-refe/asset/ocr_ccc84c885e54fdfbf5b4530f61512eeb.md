| Web Site | Name |
| --- | --- |
| fedoraproject.org/wiki/Tools/GFS | Fedora GFS resources and links |
| www.pvfs.org | Parallel Virtual File System, PVFS2 (open source) |
| sourcereare.org/gfs | Global File System (Fedora and commercial versions) |
| www.coda.cs.cmu.edu ftp.coda.cs.cmu.edu/pub/coda/linux | Coda File system, disconnected mobile access (experimental) |
| www.inter-mezzo.org | Intermezzo (open source) |
| clusterfs.com | Lustre |

TABLE 38-3 Distributed File Systems

# # Parallel Virtual File System (PVFS)

The Parallel Virtual File System (PVFS) implements a distributed network file system using a management server that manages the files system on different I/O servers. Management servers maintain the file system information, including access permissions, directory structure, and metadata information. Requests for access to a file are submitted by a client of the management server. The management server then sets up a connection between the client and the I/O servers that hold the requested file's data. Access operations such as read and write tasks are then carried out directly between the client and the I/O servers. PVFS can be implemented transparently using a kernel module to make use of the kernel's virtual file system. The PVFS file system can then be mounted by a client like any file system. In a PVFS implementation, the file system is organized into stripes of data, similar to a RAID array, but the stripes are distributed to different hosts on the network. Files are accessed as a collection of stripes that can be distributed across this network.

A new version of PVFS, known as PVFS2, is currently available from www.pvfs.org. You can download the source code from there. PVFS is a joint project with the Parallel Architecture Research Laboratory at Clemson University and the Mathematics and Computer Science Division at Argonne National Laboratory.

The PVFS manager server uses two configuration files, pvfs2-fs.conf and pvfs2-server.conf. You create these files using a configuration script, pvfs2-genconfig. The script will prompt you for configuration information such as the protocol, port, log file, and storage directory. To configure a cluster network, be sure to enter the hosts that will operate as I/O servers.

The management server is pvfs2-server. To manage the server, first place the pvfs2-server service script in the/etc/init.d directory. Then you can use the script with the service command to start and stop the server. To have the server run automatically, use chkconfig or system-config-services to turn it on.

On I/O servers, you run the pvfs2-server script to create storage space, and then start the server. The I/O servers use the /etc/pvfs2-fs.conf configuration file. You can use the pvfs2-server server script to turn the server on automatically.

On the clients that will use the PVFS system, you need to install file system configuration information and access tools. Each client will need a PVFS daemon, pvfs2-client, and its supporting module and library. File systems mount configuration can be held in /etc/pvfs2tab, though you can place entries directly in the/etc/fstab file. To mount a PVFS file system,