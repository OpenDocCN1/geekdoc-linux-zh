the option to execute binaries is a must. The final question is answered just as before, with a limited number of client systems allowed to access the mounted filesystem with root privileges and the majority not.

# The /etc/exports File

The next step in configuring your NFS server is to set up the /etc/exports file. This file defines a number of things, the first being the filesystems to make available to clients on the network. In addition to this, entries in this file define the clients that may access these shared filesystems and the type of access allowed from these clients.

To better understand the format of this file, create entries for the /home and /usr/local filesystems as previously discussed. For purposes of this example, assume that there are four clients who require access to these filesystems: gold, silver, and platinum, which are regular workstations used by non-technical users, and titanium, which is the systems administrator’s workstation. Here are the entries I would make in the /etc/exports file for these two filesystems:

```
/etc/exports
/home (rw,root_squash) titanium(rw,no_root_squash)
/usr/local (ro,root_squash) titanium(rw,no_root_squash)
```

As you can see, the format is quite simple. The line containing /home translates to /home is exported to everyone (the default since no host was specified) with read-write capability, setuid binaries disallowed, and root mapped to user nobody when the client is accessing the /home filesystem. It is also exported to the workstation titanium with the same options, with the exception that root on titanium retains root privileges when accessing the /home filesystem. The next line, which defines /usr/local as an exported filesystem, is exported read-only to everyone and root is mapped to nobody for all systems on the network with the exception of titanium, which is allowed read-write access and root equivalency.

# Setting Options for an Exported Filesystem

The next question that you should be asking is what options may be set on an exported filesystem that can be specified in the /etc/exports file. The most commonly used options and their meanings are described in Table 15.2