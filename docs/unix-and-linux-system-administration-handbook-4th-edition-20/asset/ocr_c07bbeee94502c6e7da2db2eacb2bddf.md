# Package namespaces

systems based on an open standard. For UNIX and Linux environments this is nothing new, but the DMTF is not a UNIX creature. It includes Cisco, Microsoft, Symantec, and many other companies with little history of providing sensible ways of scripting their systems. Giving these products a configuration API is a good thing, even if the implementations are still lacking.

# 12.12 Sharing software OVER NFS

Where should extra software be installed: on individual clients or on a central server from which it can be shared over NFS? The standard answer is "the clients," but the NFS makes updates quicker (it faster and more reliable to update ten servers over 1,000 clients) and save disk space on clients (not that this matters in the world of 1TB disks).

The question really boils down to manageability versus reliability. Network file-based access is centralized and easier to manage from day to day, and it makes fixes and new packages instantaneously on all clients. However, running over the network may be a bit slower than accessing a local disk. In addition, the network server adds dependencies on the network and the file server, not only because it adds potential points of failure but also because it requires clients and servers agree on things like the shared libraries that will be available and the version of those libraries will be installed. The bottom line is that NFS software libraries are an advanced administrative technique and should only be attempted in environments that allow for a high degree of central coordination.

In general, networks of heterogeneous systems derive the most benefit from shared software repositories. If your site is standardized on one operating system and that operating system provides reasonable package management facilities, you're likely to be better off sticking with the native system.

# Package namespaces

Traditional UNIX sprays the contents of new packages across multiple directories. Libraries to /usr/lib, binaries to /usr/bin, documentation to /usr/share/docs, and so on. Linux inherits more or less the same system, although Filesystem Hierarchy Standard makes the locations more predictable. (See pathname/fhs for more information about the FHS.)

The advantage of this convention is that files show up in well-known places. As your PATH environment variable points to /usr/bin and the other standard binary directories, for example, newly installed programs will be readily available.

The downsides are that the origins of files must be explicitly tracked (by means of package management systems) and that the scattered files are difficult to share over a network. Fortunately, sysadmins are willing to put in some extra work to have a reasonable way out of this dilemma: package namespaces.

![](bbox=[0.943, 0.615, 0.995, 0.715])