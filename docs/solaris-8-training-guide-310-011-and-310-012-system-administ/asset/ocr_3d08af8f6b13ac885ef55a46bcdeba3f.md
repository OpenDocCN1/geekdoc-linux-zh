You can enable WebNFS access for clients that are not part of the local subnet by configuring the firewall to enable a TCP connection on port 2049. Just allowing access for httpd does not allow NFS URLs to be used.

# CacheFS

A fundamental factor in computer performance is file access time. In a networked environment using NFS, every file access request across the network affects performance. The Cache File System (CacheFS) can be used to improve performance of NFS mounted file systems or slow devices such as a CD-ROM. When a file system is cached, the data read from the remote file system or CD-ROM is stored in a cache on the local system’s disk. First, let’s introduce some terms:

+   - **Back file system.** The file system on the remote host, or CD-ROM, that is being cached. Typically this is an NFS or HSFS file system. Files in the back file system are called back files.
- **Front file system.** The file system that contains the cached data, typically a UFS file system. Files in the front file system are called front files.
- **Cached file system.** The file system that resides on the local disk. Files in it are cached files.
- **Cache directory.** The directory on the local disk where the data for the cached file system is stored.
- **Cold cache.** A cache that does not yet have any data in its front file system. To create a cache, requested data must be copied from the back file system to the front file system. This is referred to as populating the cache. An attempt to reference data that is not yet cached is referred to as a cache miss.
- **Warm cache.** A cache that contains the desired data in its front file system. Requested data is available to the user without requiring any action from the back file system. An attempt to reference data that is already cached is referred to as a cache hit.

> NOTE
Be sure your browser supports WebNFS. If it doesn't, you'll get an error similar to the following: “NFS URLs are not supported.” Currently, Sun’s HotJava browser supports WebNFS, and Netscape says that it will provide support in a future release. Microsoft's Internet Explorer does not support WebNFS.