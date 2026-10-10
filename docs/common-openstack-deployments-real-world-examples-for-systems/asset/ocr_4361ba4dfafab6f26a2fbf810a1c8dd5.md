# 8 Block Storage Cloud

> "The road to the City of Emeralds is paved with yellow brick."
> 
> L. Frank Baum, *The Wonderful Wizard of Oz*

OpenStack provides two popular mechanisms for storage: object and block storage. Block storage is traditionally what you’d mount as a filesystem on your server. Object storage instead hosts individual files that are then referenced from within your application. In Chapter 9, “Object Storage Cloud,” you learn about why you may want to use object storage with Swift to host files. This chapter covers block storage with Cinder.

Integrated with the rest of OpenStack, Cinder volumes can be created within an OpenStack cloud and then live mounted to a specified instance at the whim of a user. Additionally, you can unmount that volume from one instance and mount it on another with just a few commands.

# ### Uses

One of the strengths of OpenStack is to avoid vendor lock-in, particularly when used in combination with versatile solutions like Cinder. Cinder provides an abstraction layer through the volume manager that hooks in to over 70 different proprietary and open source storage solutions. Additionally, it can be an interface to multiple back ends at once, enabling you to not only diversify your back ends across vendors but also change them out and do a planned migration as your organization sees fit.

# ### Cloud Provider

Whether you’re running a public cloud accessible to customers or a private cloud for use within your organization, offering the capability to extend the given filesystem requirements in place for the flavors can be a huge benefit.

With the capability to add block storage volumes on the fly, the storage requirements for default compute nodes can be kept small to preserve space for users who want to focus on the compute power and give others the flexibility to add the storage they need on the fly. The flexibility to extend storage as needed helps scaling out resources without over-committing beforehand and makes migrations easier if data is kept on a single volume that can be moved to a new compute instance.