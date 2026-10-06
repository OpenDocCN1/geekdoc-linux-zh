The NFS server will allow wild cards to say a certain network access the shares. In our case we have enabled the IBM network to access these shares by specifying *.ibm.com as the allowed hosts.

The options section tells you how the restrictions impose the mount on the NFS clients. This only applies per restriction, not to every client that accesses the NFS shares. For example, if we added .suse.de to the restrictions table, we could allow everyone at IBM to write access to the share (option rw), but read-only access to everyone at SuSE (option ro) for the same share.

See mount(5) for other options you can use.

Once you have added all of the mounts you wish to export, click Next to continue. You will be asked to confirm that you wish to use these settings. If you wish to edit them more, click No; otherwise click Yes to commit them.

# 4.7.4 Yaast2: Network services configuration

![](bbox=[0.268, 0.37, 0.849, 0.725])

Chapter 4. SuSE Linux basic system administration 113