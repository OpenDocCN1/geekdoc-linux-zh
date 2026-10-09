I strongly advise you to use your jail host only for the purpose of running jails and to put all services inside a jail. Start by configuring the host's storage to separate jails and the host operating system.

Many hosts intended for virtualization include SATA DOM flash drives on the mainboard for the operating system. These drives are usually less than 100GB in size, but a base install of FreeBSD fits in much less than a gigabyte. If you have a SATA DOM or similar, use it for the host operating system. If you have multiple sets of redundant hard drives, use a pair to mirror the operating system and dedicate everything else to jails.

If you don't have such hardware, dedicate space to the host operating system. Use either a partition for UFS filesystems or a dataset reservation for ZFS. In either case, 10GB of space should be sufficient. If you need additional space for an emergency, you can borrow some from the jail space.

While ZFS is highly useful for jails, it's not necessary. I ran jails on UFS for many years. Use what works for you and fits your environment.

Once you have your host partitioned and the operating system installed, look at the network.

# # Jail Networking

There are two seemingly conflicting aspects of jail networking: first, each jail expects full control of any IP addresses assigned to it; and second, jails can share IP addresses with other jails and even the host. You can start a jail using any IP address on the host, but that jail can't coordinate any network-facing services with other services running on that IP. If your jail shares the host's IP address, and the host runs SSH on port 22, the jail can't use port 22. If you try to start sshd(8) in the jail, the program will complain that it can't use port 22 and crash. Sharing IP addresses between jails, or even between jails and the host, requires the sysadmin to coordinate which ports belong to which hosts and to configure everything accordingly.

The simplest way to configure jails is to assign each its own IP address and give the host its own IP address. Each jail can then