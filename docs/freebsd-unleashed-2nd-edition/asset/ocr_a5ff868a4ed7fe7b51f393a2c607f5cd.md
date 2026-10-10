has mounted, and the same access permissions must apply for all shares within a filesystem. The following setup is illegal:
`/home/frank 64.41.131.102`
`/home/joe 64.41.131.102`
However, this one is correct:
`/home/frank /home/joe 64.41.131.102`

You can use the showmount program (with the -e, "show exports list" option) to display the valid shares and their permissions. This is how you can tell whether your /etc/exports setup is valid:
# showmount -e
Exports list on localhost:
/usr
/home/frank 64.41.131.102
/home/joe 64.41.131.102
/ 64.41.131.0

# Starting NFS Services Without Rebooting

The cleanest way to start NFS services is to reboot the system. However, if you need to start the services and you don't want to reboot, simply issue the following commands as root (omitting the rpcbind command if it's already running):
# rpcbind
# nfsd -u -t -n 4
# mountd -r
Then, you can use showmount -e to make sure the NFS shares are being exported properly.

# Configuring an NFS Client

If your FreeBSD machine will be mounting NFS shares from other servers, you will need to configure it as a client. Technically this isn't really necessary—you can mount an NFS share in a rudimentary fashion right out of the box. However, configuring the system as an NFS client gives you a few features that ensure speedy and reliable performance, such as the nfsiod dispatcher.

To set up an NFS client machine, simply enable the following line in /etc/rc.conf:
nfs_client_enable="YES"
This setting enables the NFS Input/Output Daemon, nfsiod, which helps to streamline NFS client requests and tunes a few kernel settings to improve access time. This is all