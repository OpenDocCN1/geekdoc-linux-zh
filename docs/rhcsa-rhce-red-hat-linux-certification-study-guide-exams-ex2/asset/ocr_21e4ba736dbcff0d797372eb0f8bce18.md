# CERTIFICATION OBJECTIVE 16.02

# Test an NFS Client

Now you can mount a shared NFS directory from a client computer. The commands and configuration files are similar to those used for any local filesystem. In the preceding section, you configured an NFS server. For now, stay on the NFS server system, as the first client test can be run directly from the server system.

# NFS Mount Options

Before doing anything elaborate, you should check for the list of shared NFS directories. Then you can test the shared NFS directory from a second Linux system, presumably a RHEL 6 system (or equivalent). To that end, the showmount command displays available shared directories.

The two options of significance are -d and -e; when coupled with the hostname or IP address of the NFS server, the command displays the shared directories, possibly including the host limits of the share. For example, given a simple share of the /mnt and /home directories on a given NFS server, the showmount -d server1.example.com command provides the following result:

```
Directories on server1.example.com:
/home
/mnt
```

As suggested, the showmount -e server1.example.com command provides more information:

```
Export list for server1.example.com:
/mnt 192.168.100.0/24
/home 192.168.122.0/24
```

If you don't see a list of shared directories, log in to the NFS server system. Repeat the showmount command, substituting localhost or 127.0.0.1 for the host name or IP address. If there's still no output, review the steps described earlier in this chapter. Make sure the /etc/exports file is configured properly. Remember to export the shared directories. Use the command

```
# /etc/init.d/nfs status
```