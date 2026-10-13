with RHEL 5. The yum command uses subscribed RHN channels and any other repositories configured in the /etc/yum.repos.d directory.

All you need to do to install the packages listed in Figure 7-4 is run the following command:

```
# yum install gcc redhat-rpm-config patchutils elfutils-libelf-devel zlib-devel binutils-devel hmaccalc
```

If so prompted, accept the request to install additional dependent packages, and then all of the noted dependencies are installed automatically. (Yes, the -y switch would perform the same function.) If updates are available from connected repositories, the latest available version of each package is installed. The yum command is described in more detail later in this chapter. But if you're running RHEL 6 without a connection to the RHN, nothing happens. Shortly, you'll see how to create a connection between yum and the installation server created in Chapter 1.

There are a number of third-party repositories available for RHEL. They include several popular applications that are not supported by Red Hat. For example, I use one to install packages associated with my laptop wireless network card.

While the owners of these repositories work closely with some Red Hat developers, there are some reports where dependencies required from one repository are unavailable from other repositories, leading to a different form of "dependency hell." However, at least the more popular third-party repositories are excellent; I've never encountered "dependency hell" from using these repositories.

![](bbox=[0.15, 0.7, 0.25, 0.8])

> > There are two main reasons why Red Hat does not include most proven and popular packages available from third-party repositories. Some are not released under open-source licenses, and others are packages that Red Hat simply chooses not to support.

# Basic yum Configuration

Relief from dependency hell depends on the proper configuration of yum. Not only do you need to know how to configure yum to connect to repositories over the Internet, but also you need to know how to configure yum to connect to repositories on a local network. With this knowledge, you can connect yum to repositories on the RHN, to repositories configured by third parties, and to custom repositories configured for specialized networks. And remember, during the Red Hat exams, you won't have access to the Internet.