
The above command will display output containing a line for each guest similar to the following:

virsh # list

| Id | Name | State |
|----|------|-------|
| 8 | RHEL9VM | running |
| 9 | CentOS9VM | running |
| 10 | FedoraVM | running |

## 26.3 Starting a Guest System

A guest operating system can be started using the virsh tool combined with the start option followed by the name of the guest operating system to be launched. For example:

```
# virsh start myGuestOS
```

## 26.4 Shutting Down a Guest System

The shutdown option of the virsh tool, as the name suggests, is used to shut down a guest operating system:

```
# virsh shutdown guestName
```

Note that the shutdown option allows the guest operating system to perform an orderly shutdown when it receives the instruction. To instantly stop a guest operating system, the destroy option may be used (with the risk of file system damage and data loss):

```
# virsh destroy guestName
```

## 26.5 Suspending and Resuming a Guest System

A guest system can be suspended and resumed using the virsh tool's suspend and resume options. For example, to suspend a specific system:

```
# virsh suspend guestName
```

Similarly, to resume the paused system:

```
# virsh resume guestName
```

A suspended session will be lost if the host system is rebooted. Also, be aware that a suspended system continues to reside in memory. Therefore, to save a session such that it no longer takes up memory and can be restored to its exact state (even after a reboot), it is necessary to save and restore the guest.

## 26.6 Saving and Restoring Guest Systems

A running guest operating system can be saved and restored using the virsh utility. When saved, the current status of the guest operating system is written to disk and removed from system memory. A saved system may subsequently be restored at any time (including after a host system reboot).

To save a guest:

```
# virsh save guestName path_to_save_file
```

To restore a saved guest operating system session:

```
# virsh restore path_to_save_file
```

## 26.7 Rebooting a Guest System

To reboot a guest operating system:

```
# virsh reboot guestName
```

## 26.8 Configuring the Memory Assigned to a Guest OS

To configure the memory assigned to a guest OS, use the setmem option of the virsh command.

For example, the following command reduces the memory allocated to a guest system to 256MB:

```
# virsh setmem guestName 256
```

Note that acceptable memory settings must fall within the memory available to the current Domain. This may be increased using the setmaxmem option.

## 26.9 Summary

The virsh tool provides various options for creating, monitoring, and managing guest virtual machines. As outlined in this chapter, the tool can be used in either command-line or interactive modes.

## Chapter 27

## 27. An Introduction to Linux Containers

The preceding chapters covered the concept of virtualization, emphasizing creating and managing virtual machines using KVM. This chapter will introduce a related technology in the form of Linux Containers. While there are some similarities between virtual machines and containers, key differences will be outlined in this chapter, along with an introduction to the concepts and advantages of Linux Containers. The chapter will also overview some RHEL 9 container management tools. Once the basics of containers have been covered in this chapter, the next chapter will work through some practical examples of creating and running containers on RHEL 9.

### 27.1 Linux Containers and Kernel Sharing

In simple terms, Linux containers are a lightweight alternative to virtualization. A virtual machine contains and runs the entire guest operating system in a virtualized environment. The virtual machine, in turn, runs on top of an environment such as a hypervisor that manages access to the physical resources of the host system.

Containers work by using a concept referred to as kernel sharing, which takes advantage of the architectural design of Linux and UNIX-based operating systems.

To understand how kernel sharing and containers work, it helps first to understand the two main components of Linux or UNIX operating systems. At the core of the operating system is the kernel. The kernel, in simple terms, handles all the interactions between the operating system and the physical hardware. The second key component is the root file system which contains all the libraries, files, and utilities necessary for the operating system to function. Taking advantage of this structure, containers each have their own root file system but share the host operating system's kernel. This structure is illustrated in the architectural diagram in Figure 27-1 below.

This type of resource sharing is made possible by the ability of the kernel to dynamically change the current root file system (a concept known as change root or chroot) to a different root file system without having to reboot the entire system. Linux containers are essentially an extension of this capability combined with a container runtime, the responsibility of which is to provide an interface for executing and managing the containers on the host system. Several container runtimes are available, including Docker, lxd, containerd, and CRI-O. Earlier versions of RHEL used Docker by default, but Podman has supplanted this as the default in RHEL 9

![](img/be1f159c3cc937d7b264dc5b134856dc_218_0.png)

Figure 27-1

### 27.2 Container Uses and Advantages

The main advantage of containers is that they require considerably less resource overhead than virtualization allowing many container instances to be run simultaneously on a single server. They can be started and stopped rapidly and efficiently in response to demand levels. In addition, containers run natively on the host system providing a level of performance that a virtual machine cannot match.

Containers are also highly portable and can be easily migrated between systems. Combined with a container management system such as Docker, OpenShift, and Kubernetes, it is possible to deploy and manage containers on a vast scale spanning multiple servers and cloud platforms, potentially running thousands of containers.

Containers are frequently used to create lightweight execution environments for applications. In this scenario, each container provides an isolated environment containing the application together with all of the runtime and supporting files required by that application to run. The container can then be deployed to any other compatible host system that supports container execution and runs without any concerns that the target system may not have the necessary runtime configuration for the application - all of the application's dependencies are already in the container.

Containers are also helpful when bridging the gap between development and production environments. By performing development and QA work in containers, they can be passed to production and launched safely because the applications run in the same container environments in which they were developed and tested.

Containers also promote a modular approach to deploying large and complex solutions. Instead of developing applications as single monolithic entities, containers can be used to design applications as groups of interacting modules, each running in a separate container.

One possible drawback of containers is that the guest operating systems must be compatible with the version of the kernel being shared. It is not, for example, possible to run Microsoft Windows in a container on a Linux system. Nor is it possible for a Linux guest system designed for the 2.6 version of the kernel to share a 2.4 version kernel. These requirements are not, however, what containers were designed for. Rather than being seen as limitations, these restrictions should be considered some of the key advantages of containers in providing a simple, scalable, and reliable deployment platform.

### 27.3 RHEL 9 Container Tools

RHEL 9 provides several tools for creating, inspecting, and managing containers. The main tools are as follows:

- **buildah** – A command-line tool for building container images.
- **podman** – A command-line based container runtime and management tool. Performs tasks such as downloading container images from remote registries and inspecting, starting, and stopping images.
- **skopeo** – A command-line utility used to convert container images, copy images between registries and inspect images stored in registries without downloading them.
- **runc** – A lightweight container runtime for launching and running containers from the command line.
- **OpenShift** – An enterprise-level container application management platform consisting of command-line and web-based tools.

All of the above tools comply with the Open Container Initiative (OCI), a set of specifications designed to ensure that containers conform to the same standards between competing tools and platforms.

### 27.4 Container Catalogs, Repositories, and Registries

The Red Hat Container Catalog (RHCC) provides a set of pre-built images tested by Red Hat that can be downloaded and used as the basis for your own container images. The RHCC can be accessed at the following URL and allows searches to be performed for specific images:

https://catalog.redhat.com/software/containers/search

After completing a search, the catalog will display a list of matching repositories. A repository in this context is a collection of associated images. Figure 27-2, for example, shows a partial list of the container image repositories available for RHEL 9 related containers:
