9

# Object Storage Cloud

> > "I paint objects as I think them, not as I see them."
> > Pablo Picasso

As explained in Chapter 8, “Block Storage Cloud,” OpenStack provides two core ways for handling storage: object and block storage. Block storage is typically where you mount a storage device as an actual filesystem on your server. Object storage instead hosts individual files that are then referenced from within your application and accessed using a REST API. This means that instead of hosting files on a flat filesystem as in block storage, object storage enables storing of individual files, or objects, in a highly redundant and available storage system. Using an object store also enables you to tune access to these files through access control and make them selectively available across your platform.

This chapter walks you through the key concepts of using OpenStack Swift. From there, you create a very basic object storage configuration on your controller that you can then access and interact with via the Horizon dashboard and from your compute node.

# Uses

Swift object storage was one of the two original OpenStack projects, the other being Nova. The fact that it was one of the original projects demonstrates how important object storage is to the vision of many cloud deployments.

As soon as object storage is made available to an organization, uses for it start cropping up. From building a system of shared documents around an object store or giving flexibility to developers to include files in their applications without having to worry about data access or integrity, being able to store files on a trusted, redundant storage system is valuable throughout an organization.

# Web Hosting Company

There have been many strategies that web hosting companies have employed over the years to make their platforms highly available and make the most efficient use of resources. One of the latest is storing images and other binary objects in a managed object store rather than hosting them on individual filesystems.