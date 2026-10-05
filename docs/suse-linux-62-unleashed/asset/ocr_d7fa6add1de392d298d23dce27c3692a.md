# NFS
CHAPTER 15

# Caution

Unfortunately, NFS's design is insecure by nature. Although taking some steps to protect yourself from the common user pretending to be an evil hacker provides a moderate level of security, there is not much you can do. Any time you share a disk with another machine via NFS, you need to give the users of that machine (especially the root user) a certain amount of trust. If you believe that the person you are sharing the disk with is untrustworthy, you need to explore alternatives to NFS for sharing data and disk space.

Keep up with security bulletins from both SuSE and the Computer Emergency Response Team (CERT). You can find these bulletins on SuSE's site at www.suse.com, CERT's site at www.cert.org, or the moderated newsgroup comp.security.announce.

# Installing NFS

Although the NFS software comes preinstalled with SuSE Linux, you need to be aware of what the software is and what each specific program does. This is important when you are troubleshooting problems and configuring NFS-related tools, such as the automounter.

Three programs provide NFS server services:

+   - **portmap**: This program does not directly provide NFS services itself, however, it calls made from other machines to the correct NFS daemons.

+   - **rpc.nfsd**: This daemon is what translates NFS requests into actual requests on the local filesystem.

+   - **rpc.mountd**: This daemon services requests to mount and unmount filesystems.

# Note

The rpc.nfsd and rpc.mountd programs need only run on your NFS servers. In fact, you might find prudent not to run them all on your client machines, for security concerns and to free resources that might otherwise be consumed by them. NFS clients do not need any special NFS software to run. They should run the portmap program, however, because it provides RPC functionality to programs other than NFS.

![](bbox=[0.845, 0.785, 0.995, 0.925])