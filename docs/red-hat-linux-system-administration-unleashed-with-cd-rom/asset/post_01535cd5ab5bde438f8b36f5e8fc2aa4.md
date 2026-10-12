
## Network File Services

Next to printers, the most commonly shared resources on a network are filesystems and the standard method for doing this on Linux systems is with NFS. In the earlier releases of Linux, NFS was implemented using a daemon that ran in user space. This design worked but it was inefficient and prone to errors, which gained Linux the reputation of being a poor choice for an NFS server. This inefficiency led developers to look for a better solution and during the development phase of the 2.1 kernel, a team of programmers including Olaf Kirch, H.J. Lu, Rick Sladkey, Linus, and many others, implemented kernel space NFS. There were naturally a number of bumps along the way, but this implementation is changing the way that people look at NFS under Linux. The kernel space NFS support is dramatically better than the user space daemon. It is more efficient and more compliant with the NFS specification. Along with this NFS implementation, for the first time a locking daemon was implemented, which solved the biggest drawback to using Linux as an NFS server. With the 2.2 kernel, such as the one that comes with Red Hat Linux 6, Linux NFS is much improved and continues to improve all the time.

This section looks at what is required to set up Linux as an NFS server, examines the /etc/exports file, and looks at how simple it is to use Linux as an NFS client. Finally, the end of this section looks at a couple of other network filesystems, or more correctly, distributed filesystems (AFS and Coda) that are available for Linux and compares and contrasts their features with those of NFS.

## NFS Server Configuration

When deciding to set up an NFS server under Linux, the first decision is whether to use the older user space NFS implementation or to use the kernel NFS support. By default, Red Hat will use the newer kernel space NFS daemon. However, if you are moving from an older version of Linux, you can continue to use the user space NFS implementation. The drawback to not using the kernel space NFS is that you will not have lockd support. If you choose to use the user space NFS method, you can refer to the NFS-Howto from the Linux Documentation Project, which has yet to be updated to cover the new NFS implementation.

## Installing NFS Related Software

Assuming that you selected NFS server support during the installation of your Red Hat server, you will not have to install any software in order to set up an NFS server. But if you didn’t, you will need to install the following RPM packages in order to get started:

- knfsd
- knfsd-clients
- portmap

Once these packages are installed, you will need to ensure that your kernel includes support for networking and the NFS filesystem type. There are two options associated with running the kernel space NFS server, the first being the CONFIG_NFSD. This option is not required if you are just running the user space NFS daemon, but it is an absolute must if you want to use the kernel NFS daemon support. An additional option that you may choose to set is to emulate the behavior of the Sun NFS server. This option is CONFIG_NFSD_SUN and you may set it or not depending on your requirements. An explanation of this option is available via the Help option when configuring the kernel. Once you have made the appropriate kernel configuration choices, you must rebuild and install your new kernel. Kernel configuration and building is discussed in Chapter 35, “Customizing the Linux Kernel,” if you need help with this. Naturally, a new kernel means a reboot in order to activate it.

## Finalizing the Setup of NFS

Now that you have the kernel configured, you are ready to proceed with the remaining steps in setting up your NFS server. The first of these steps is to decide which filesystems you want to share via the network. This may sound easy enough, but you must also make several decisions as to what capabilities users on other systems will have when accessing the shared filesystems. These decisions include the following:

- Do client systems require write access to the filesystem?
- Should users be able to run setuid programs that reside on the filesystem?
- Should users be able to run any programs that reside on the shared filesystem?
- Should the root user on client systems have root privileges when accessing the filesystem?

The answers to these questions are very important because they have a significant impact on the security of your systems. This is because the NFS filesystem is inherently a security risk. Failure to consider these issues may mean that you have inadvertently opened security holes in your system. Let’s take a look at a couple of examples and how we would answer these questions for each of them.

> Note
> 
> You may be asking why I state that NFS is inherently a security risk. There are a number of reasons for this, but the primary one is that no authentication is required or supported for client interaction with the NFS server. This means that if you export a filesystem to clients on your network and do not restrict access to a specific set of systems, any system on the network with an NFS client can access the files contained on the filesystem. This is in contrast to other network filesystems such as AFS, which uses Kerberos to authenticate users before granting access.

## Sharing the /home Filesystem

The first filesystem we want to share is the /home filesystem. Sharing the /home filesystem allows users to access their personal files from all of the machines on the network, which is a desirable feature of most networks. The answer to the first question as to whether client systems require write access to the filesystem is obviously yes because a home directory for a user without it would not be very useful. The answer to the next question should also be a no-brainer. The /home filesystem is an unsafe place from which to run setuid binaries, especially with the proliferation of email attachment trojans and other binaries from the Internet of unknown origin. This brings us to the third question. This question is less clear cut and is somewhat dependent on your user base. If all of your users are non-technical, you may be able to get away with not allowing the execution of programs residing on the /home filesystem. However, if you have a more sophisticated user base, they will invariably have favorite scripts and programs that they want to run from a personal binary directory. The final question is whether the root user on client machines should have root privileges when accessing the /home filesystem. The answer to this question usually depends on the role of the client system. For example, if the client system is a systems administrator's workstation, you may want to allow root on that system to equate to root on the NFS server system. If, on the other hand, the client system is used by the receptionist, you probably do not want root on this client to have root privileges on the mounted filesystem.

## Sharing the /usr/local Filesystem

Here's a look now at another filesystem that you might want to share on the network, /usr/local. Unlike the /home directory, in which the client systems would need read and write access to the filesystem, only a limited number of systems will need this type of access in this case. The default option is for clients to mount it read-only. Because this is the case, and because the filesystem is likely to contain a significant number of binaries installed by the systems administrator, you can more safely install setuid binaries in this filesystem and the option to execute binaries is a must. The final question is answered just as before, with a limited number of client systems allowed to access the mounted filesystem with root privileges and the majority not.

## The /etc/exports File

The next step in configuring your NFS server is to set up the /etc/exports file. This file defines a number of things, the first being the filesystems to make available to clients on the network. In addition to this, entries in this file define the clients that may access these shared filesystems and the type of access allowed from these clients.

To better understand the format of this file, create entries for the /home and /usr/local filesystems as previously discussed. For purposes of this example, assume that there are four clients who require access to these filesystems: gold, silver, and platinum, which are regular workstations used by non-technical users, and titanium, which is the systems administrator’s workstation. Here are the entries I would make in the /etc/exports file for these two filesystems:

/etc/exports
/home (rw,root_squash) titanium(rw,no_root_squash)
/usr/local (ro,root_squash) titanium(rw,no_root_squash)

As you can see, the format is quite simple. The line containing /home translates to /home is exported to everyone (the default since no host was specified) with read-write capability, setuid binaries disallowed, and root mapped to user nobody when the client is accessing the /home filesystem. It is also exported to the workstation titanium with the same options, with the exception that root on titanium retains root privileges when accessing the /home filesystem. The next line, which defines /usr/local as an exported filesystem, is exported read-only to everyone and root is mapped to nobody for all systems on the network with the exception of titanium, which is allowed read-write access and root equivalency.

## Setting Options for an Exported Filesystem

The next question that you should be asking is what options may be set on an exported filesystem that can be specified in the /etc/exports file. The most commonly used options and their meanings are described in Table 15.2
