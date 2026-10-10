to make it too high, since it increases replication time. Also note that these partitions are different than the disk partitions you are already familiar with.

+   - **Replicas**—These control how many times you want Swift to store your data across the cluster to ensure redundancy. The default is three.

This is a very basic introduction to Rings. The Swift Developer documentation located at http://docs.openstack.org/developer/swift/ contains a considerable amount of documentation that dives deep into storage decisions, Ring preparation and management and more. Of particular interest with regard to Rings are the “Swift Architectural Overview,” which provides more detail about where the Rings play a role in a high level and “The Rings” section of the manual, which provides an in-depth description of the Rings. Finally, you will want to reference the “Deployment Guide” section of the Administrator Documentation, which provides an overview of service distribution and steps for manual Ring creation, manipulation and distribution.

# Objects and Containers

As we’ve discussed, Swift is an object storage system. An object is a file of any type that you wish to store somewhere. This may be an image, a log, an mp3 or anything else. These objects are stored in what Swift calls a container, which is a collection of objects. A container has specific attributes to define who has access to it and whether it is publicly available. These containers are stored in what Swift calls an account, which is a collection of containers. Accounts are the root storage location for data.

> **Container: An Overloaded Term**
> 
> In Chapter 11, “Controlling Containers,” we discuss using containers in OpenStack, but these are different containers than we talk about here.
> 
> As you can see from the architecture diagram, Swift has a concept of containers, referring to where you will place objects. However, broadly speaking, in OpenStack and in our later chapter, containers instead refer to technologies like Docker and Kubernetes, which provide an isolated operating system environment for running applications.
> 
> As you’ll see later in this chapter, the container term in OpenStack Client (OSC) refers to the usage in Swift.
> 
> While we’re on the topic of overloaded terms, there are a couple more. Regions in Swift are different than regions in Keystone. As briefly mentioned earlier, partitions in Swift are also not the same thing as your standard disk partitions.

# Connecting to Swift

Interaction with Swift, like other components of OpenStack, is done through the API. The API communicates with a Swift proxy, which looks up the location of the account, container, or object in the ring and will complete the action accordingly. A basic demonstration of how this works is shown in Figure 9.2. While not shown in the figure, note that a cluster is made up of multiple servers all containing objects which are replicated across the cluster.