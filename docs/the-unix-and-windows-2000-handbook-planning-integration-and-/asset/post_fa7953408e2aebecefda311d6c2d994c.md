
Once you’ve set up your secondary /usr/local servers, be aware of what systems are using them. If you have servers that have high user load, or make overly frequent use of programs in /usr/local, you may want to consider installing a local copy of /usr/local on those systems. While there is nothing wrong with running programs out of /usr/local over the network, you’ll find that users get better response with a local /usr/local, and you’ll see less load on your network. The only penalties you’ll pay for having local /usr/locals are the disk space you’ll consume and the incremental work needed to manage an additional /usr/local. If you have the disk space available on the local machine, don’t be afraid to install /usr/local.

Finally, designing your /usr/local infrastructure is very similar to designing your DNS and NFS infrastructure, but there is one major difference. Unlike DNS and NFS, there are no automated functions built into the operating system to manage the replication of your /usr/local information. However, there are operating system tools that you can use to automate this process. For more information on how to keep your /usr/local copies synchronized, see the section titled “UNIX File Management Tool,” presented later in this chapter.

## Organizing a Multi-vendor /usr/local Structure

While trying to keep up with a single /usr/local is a task in itself, what happens when you have a mixed environment that contains systems from multiple UNIX vendors? Providing a common cross-platform environment to your users, one in which all the tools they’re used to are available on every platform, is well worth the investment of your time. Constructing a multi-vendor /usr/local is not as difficult as it may seem. You’ll still need to follow the key concepts presented in the previous section, but you will have to wrap some additional design and process around those concepts to be successful.

The additional design piece involves identifying multiple systems to be your /usr/local masters. For each UNIX vendor in your environment, you’ll need to identify a system to provide resources for building, testing, and storing your master /usr/local for that UNIX vendor. Once that is in place, you can identify additional servers, similar to a single-vendor environment. However, if you have sufficient resources, namely disk space, you may consider housing your entire multi-vendor /usr/local directory structure on one system. While this may seem a strange concept since you can’t compile and test other operating system types on this system, there are two very good reasons to manage your /usr/local in this way:

- This allows you to identify a single system as your /usr/local master, helping to avoid confusion. You still need other vendor systems identified to compile and test your /usr/local programs.

Use NFS mounts to mount /usr/local from the master system to the compile and test systems.

Distributing /usr/local to secondary servers is much simpler, as the process you put in place to distribute updates to secondary /usr/locals can be managed from a single machine. This will help you keep your entire vendor /usr/local directory structure synchronized, providing your users with a consistent cross-platform environment.

## ORGANIZING VENDOR APPLICATIONS

While utilities and programs stored in /usr/local will be used by the vast majority of your users, there will be times when software packages will only be needed by subsets of your user communities. In many of these cases, the software is a specialized vendor application that only needs to be installed on a limited number of systems and used by a small group of users.

In these cases, installing these packages in /usr/local most likely is not the best option, for if you install every software package in /usr/local, you'll quickly run out of disk resources before you run out of applications you'll want to put there.

There are a few key factors to consider when planning and installing vendor applications:

- Keep them separate from the operating system's disk and directory structure. Vendor applications can be very complex and consume ample amounts of disk resources. Keep them separate from your operating system, and they won't impact your procedures for upgrading and maintaining your operating system.

- Install vendor applications with portability in mind. As applications age, new releases tend to consume more disk resources than previous releases. Try to install your applications in locations that have ample resources to handle growth over time. However, if this is not possible, you'll need to plan for the time when you'll need to move the application to a new filesystem, or even a new computer system that has added resources.

- Use symbolic links for version and location management. Employ the same process as installing utilities in /usr/local when you install vendor applications. Use symbolic links to make version management transparent to users, as well as to minimize the impact if you have to move the application to another location.

Avoid installing vendor applications on your operating system disk whenever resources permit. Over time, new vendor releases will need to be
