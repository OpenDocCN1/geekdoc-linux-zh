# ### 10.7.1 NFS Setup

The NFS setup dialog (Figure 10–7, NFS Setup Dialog) applies only if you are installing from an NFS server (that is, if you booted from a network or PCMCIA boot disk and selected NFS Image in the Installation Method dialog).

# **Figure 10–7 NFS Setup Dialog**

![](bbox=[0.13, 0.34, 0.77, 0.61])

Enter the fully-qualified domain name or IP address of your NFS server, and the name of the exported directory that contains the Red Hat Linux installation files or CD. For example, if you’re installing from a host named `east.coast` in the domain `redhat.com`, enter `east.coast.redhat.com` in the `NFS Server` field.

If the NFS server has the Red Hat Linux CD mounted on /mnt/cdrom, enter /mnt/cdrom in the Red Hat directory field. If the NFS server is exporting a mirror of the Red Hat Linux installation tree instead of a CD, enter the directory which contains the RedHat directory. For example, if your NFS server contains the directory /mirrors/redhat/i386/RedHat, enter /mirrors/redhat/i386.