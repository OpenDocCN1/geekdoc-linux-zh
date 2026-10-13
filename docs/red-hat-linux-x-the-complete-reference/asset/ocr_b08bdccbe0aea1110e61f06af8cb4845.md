```
directory-pathname  host-designation (options)
```

# NFS Host Entries

You can have several host entries for the same directory, each with access to that directory:

```
directory-pathname  host (options)  host (options)  host (options)
```

You have a great deal of flexibility when specifying hosts. For hosts within your domain, you can just use the hostname, whereas for those outside, you need to use a fully qualified domain name. You could also just use the host's IP address. Instead of just a single host, you can reference all the hosts within a specific domain, allowing access by an entire network. A simple way to do this is to use the * for the host segment, followed by the domain name for the network, such as *.mytrek.com for all the hosts in the mytrek.com network. Instead of domain names, you could use IP network addresses using a CIDR format where you specify the netmask to indicate a range of IP addresses. You can also use an NIS netgroup name to reference a collection of hosts. The NIS netgroup name is preceded by a @ sign.

```
directory      host (options)
directory      *(options)
directory      *.domain (options)
directory      192.168.1.0/255.255.255.0 (options)
directory      @netgroup (options)
```

# NFS Options

Options in /etc/exports operate as permissions to control access to exported directories. Read-only access is set with the ro option, and read/write with the rw option. The sync and async options specify whether a write operation is performed immediately (sync) or when the server is ready to handle it (async). By default, write requests are checked to see if they are related, and if so, they are written together (wdelay). This can degrade performance. You can override this default with no_wdelay and have writes executed as they are requested. If two directories are exported, where one is the subdirectory of another, the subdirectory is not accessible unless it is explicitly mounted (hide). In other words, mounting the parent directory does not make the subdirectory accessible. The subdirectory remains hidden until also mounted. You can overcome this restriction with the no_hide option (though this can cause problems with some file systems). If an exported directory is actually a subdirectory in a larger file system, its parent directories are checked to make sure that the subdirectory is the valid directory (subtree_check). This option works well with read-only file systems but can cause problems for write-enabled file systems, where filenames and directories can be changed. You can cancel this check with the no_subtree_check option.

**Table 36-1: The /etc/exports Options**

| General Options | Description |
|---|---|
| secure | Requires request originate on secure ports, those less than 1024. This is on by default. |
| insecure | Turns off the secure option. |
| ro | Allows only read-only access. This is the default. |
| rw | Allows read/write access. |
| sync | Performs all writes when requested. This is the default. |
| async | Performs all writes when the server is ready. |