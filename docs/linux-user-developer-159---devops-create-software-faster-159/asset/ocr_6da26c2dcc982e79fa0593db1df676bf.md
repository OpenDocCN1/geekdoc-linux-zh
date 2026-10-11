# Run complex container clusters on CoreOS

Read on and discover how CoreOS uses containers to manage installed software simply

![](bbox=[0.06, 0.27, 0.19, 0.41])

**Nitish Tiwari**

is a software developer by profession and an open source enthusiast by heart. As well as writing for leading open source magazines, he helps firms set up and use open source software for their business needs

**Resources**

**CoreOS**
coreos.com

Containers are the standard for running software these days, so it was high time an operating system based on containers appeared. With CoreOS, this gap has been filled very well. Let’s dig a little deeper to try and understand why a new Linux distro is needed at all when the current ones handle containers well.

The problem is the fact that, while it is easy to use containers on current Linux distros, they don’t play well when you need to manage (launch/destroy) several containers or link containers to create different back-end services. The new wave of containerisation, led by Docker, has made things lot easier – applications can now be easily deployed on almost any system. You just need the appropriate Dockerfile and Docker installation.

But, if there are several hundreds of containers and you need to up/down-scale them frequently, current distros feel insufficient. CoreOS helps you address such scenarios.

Designed for security, consistency, and reliability, CoreOS is a Linux-based operating system for clusters. It is important to mention here that CoreOS doesn’t ship with a package manager at all; rather, it comes with Docker pre-installed. You can use CoreOS to manage your services (using containers) instead of installing packages. So, for every service that you need, just create and use a container.

**Right** CoreOS integrates well other with distributed apps like etcd, rkt, fleet, flannel, etc

# 01 Preconditions

CoreOS is supported on almost all the major computing platforms – cloud providers like Amazon EC2, Azure, DigitalOcean, Google Compute Engine; virtualisation platforms like VMware, VirtualBox; cloud-based operating systems like OpenStack; bare metal servers and even your own personal computer. But, since CoreOS disk installer deletes everything on the target disk before installation, installing CoreOS on your current computer is a big ask – not everyone would want to abandon their current setup to install a new OS. It would be easier to get started with CoreOS by first trying it out on a virtual machine and then using it in full glory by installing it on a cloud server. So, we will focus on installation of CoreOS as a virtual machine on your laptop using VirtualBox to learn its features.

The first precondition is having VirtualBox installed on your system. You can download the installer for your current OS from virtualbox.org. VirtualBox is available for all the major operating systems. The next thing is the CoreOS ISO file. This is the file we will use to mount CoreOS media on VirtualBox. You can get the latest stable revision of CoreOS from: coreos.com/os/docs/latest/booting-with-iso.html.

![](bbox=[0.2, 0.62, 0.92, 0.91])