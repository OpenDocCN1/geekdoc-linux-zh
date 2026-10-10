with Fedora. When you are happy, you can use the Live CD to give you a base Fedora installation. Just double-click the Install icon on the desktop and follow the installation instructions found later in this chapter. For now, download and burn the Live CD ISO file to a blank CD using your favorite CD-burning application—it will come in handy later!

# ### Planning Partition Strategies

If you are a diehard Windows user, partitioning is something that might never have entered your mind. But simply, it is the efficient layout of information on your hard drive, and it is certainly worth giving thought ahead of the installation as to how you want to partition your drive.

# What Is a Partition?

> It can be difficult to explain to new users about *partitions*. A useful analogy is of a kitchen, in which there are many different drawers and cupboards. Imagine the kitchen is your hard drive, and the drawers and cupboards are partitions. In one cupboard, you may keep cups, another might hold ingredients, yet another may hold pots and pans. They are all part of the kitchen but have specific roles within the kitchen.
> 
> Taking this back to your hard drive, you may have a partition to hold your user information, another partition to hold the files you will use for serving web pages, and another for boot information.

Typically, Fedora creates three partitions on your drive: a `/boot` partition that stores information to help Fedora boot up, a `/partition` (or root partition) that stores the bulk of your information, and a swap partition that Fedora uses to temporarily store information when your RAM is full. For the majority of people this is fine, and many users go ahead and use the default partition options. However, there may be occasions when you want to store your `/home?` directory (which contains your user settings and documents) on a separate partition. This might be the case if you plan on upgrading your distribution fairly often and don't want to lose settings unique to you. You should be mindful of not only the current business requirements, but also any anticipated requirements, especially if you are in a growing company. It can be very painful when you are running out of storage space because you underestimated storage or partitioning requirements.

Knowing how software is allocated on your hard drive for Linux involves knowing how Fedora organizes its *file system*—its layout of directories on storage media. This knowledge can help you make the most out of hard drive space; and in some instances, such as planning to have user directories mounted via NFS or other means, it can help head off data loss, increase security, and accommodate future needs. Create a great system, and you'll be the hero of information services.