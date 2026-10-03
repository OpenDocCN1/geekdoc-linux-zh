# Chapter Summary

By now you should have a good understanding of what NFS is and how to share resources on an NFS server. You should understand the security issues associated with using NFS and know how to share NFS resources so that only authorized users can access them. There are many options available when sharing resources on an NFS server. The system administrator needs to understand each of them and make informed decisions when sharing resources, so that system security is not compromised.

Accessing resources on the NFS client from a server were discussed. I described AutoFS and the many options available when mounting NFS resources so that user downtime is minimized by unplanned system outages and unavailable resources.

Finally, I described how to maximize efficiency and system performance on NFS mounted resources using AutoFS and CacheFS.

When managing NFS, and especially automounter, a system administrator can quickly become overwhelmed with all the configuration files that must be kept consistent across the many different systems. For example, the /etc/auto_master and the related direct and indirect map files must be updated whenever the name of a host or file system changes. This can be nearly impossible on a large network. Chapter 18, describes how Network Information Services (NIS) can be used to help manage all these configuration files, including/etc/passwd and /etc/hosts, from a single location.

# KEY TERMS

+   - NFS
- NFS server
- NFS client
- Dynamic failover (as it relates to NFS)
- WebNFS
- NFS daemons
- Shared resource
- Hard mount
- Soft mount
- Replication
- NFS logging
- WebNFS
- Back file system
- Front file system
- Cached file system
- Cache directory
- Cold cache
- Warm cache
- Consistency checking
- AutoFS Maps (know each of them)
- Trigger point