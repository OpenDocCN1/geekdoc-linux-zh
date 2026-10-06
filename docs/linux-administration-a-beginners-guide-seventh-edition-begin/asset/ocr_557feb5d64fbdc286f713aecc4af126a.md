# Linux Administration: A Beginner's Guide

three lines. In addition, note that the second, third, and fourth lines begin with a pound sign (#), which means the rest of the line is commented out.

Given this format, you can see that the maps configured to be shared are passwd, group, hosts, rpc, services, netid, protocols, and mail. These entries correspond to the filenames in the preceding section of the Makefile. Of course, not all sites use these entries, or they want some additional maps shared (such as the Automunter files, auto.master, and auto.home). To change any of the maps you want, alter the line so that the maps you want are listed after a # symbol.

For example, let's say you want the passwd and group maps shared over NIS. You'd change the all: line to read as:

```
all: passwd \
# hosts rpc services protocols netgrp mail \
# shadow publish ethers bootparams amd.home \
# passwd.adunct\...
```

Note that the order of the maps in the all: line doesn't matter. The placement of the foregoing entries makes them easy to read.

# Using ypinit

Once you have the Makefile ready, you need to initialize the YP (NIS) server using the ypinit command. On your 64-bit server, this is the command:

```
[root@server-A ~#] /usr/lib64/yp/ypinit -m
```

If you are running a 32-bit Linux distro or one of the Debian Linux variants, the path to the ypinit command may be slightly different. On a 32-bit Fedora, RHEL, or CentOS server, the path is /usr/lib/yp/ypinit).

> NOTE that you must already have the NIS domain name set before you run the ypinit command. You set it with the domainname, as shown in "Establishing the Domain Name" earlier in this chapter.

In the preceding 64-bit server command, the -m option tells you to set up the system as a NIS server. Assuming we are running this command on our sample system named server-A, we would see the system respond as follows:

At this point, we have to construct a list of the hosts which will run NIS servers. server-A.example.org is in the list of NIS server hosts. Please continue to add the names for the other hosts, one per line.

When you are done with the list, type a <control D>.
ext host to add: server-A.example.org
ext host to add: