If your Ubuntu host gets an error about wrong file system type, you likely haven't installed NFS client support on your system. Just run

```
$ sudo apt-get install nfs-common
```

and try the mount command again.

# NFS User Permissions

One interesting and controversial feature of NFS is how it handles user permissions. When you mount an NFS share, the file ownership will be based on the user IDs of the users on the NFS server. For users on a remote system to be able to read and write to the share, their user IDs need to match up with the NFS server. If you use LDAP or some other system to keep user IDs consistent across servers, this shouldn't present much of a problem, but if, for instance, the ubuntu user on my NFS server had a user ID of 1000 but the ubuntu user on my client had a user ID of 1001, the client wouldn't be able to write to the mount point.

Another matter of interest with NFS permissions is how it handles root. On Ubuntu by default the root account will be squashed, because NFS blocks any attempts by a remote root user to access shares with its root privileges. Otherwise any host on the network with an Ubuntu live CD could boot it, mount the NFS share, and read and write to any files on that share, regardless of the permissions. With this security issue in mind, you still might want to disable root squashing. To do so, add the no_root_squash option to your list of export options in /etc/exports. Each option is separated by commas, so if I wanted to disable root squashing on the share I created earlier, the file would look like the following:

```
/mnt/share 192.168.1.0/255.255.255.0(rw,no_root_squash)
```

# Edubuntu and LTSP

The community-driven Edubuntu project aims to create an add-on for Ubuntu specially tailored for use in primary and secondary education. Edubuntu exists as a platform for tools for teachers and administrators. But the real thrust, of course, and the real purpose, is to put free and open source software into the hands of children. In doing so, Edubuntu provides