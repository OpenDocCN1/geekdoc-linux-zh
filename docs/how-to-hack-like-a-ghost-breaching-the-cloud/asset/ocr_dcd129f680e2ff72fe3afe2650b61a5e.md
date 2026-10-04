The child's CapEff list is equal to its CapPrm if the file has the effective bit set; otherwise, it gets populated by CapAmb. Inheritable capabilities (CapInh) and bounded capabilities (CapBnd) are transferred as is to the child process.

Before you start loading your shotgun, know that I only wrote this to demonstrate how tricky it is to determine the set of capabilities assigned to a new process. I encourage you to dive deeper into the subject and learn how to leverage capabilities in containers. You can start with Adrian Mouat's excellent introduction “Linux Capabilities: Why They Exist and How They Work” at https://blog.container-solutions.com/ and the official Linux kernel manual page on capabilities in Section 7 of https://man7.org/.

# Docker Socket

Next we look for the /var/run/docker.sock file, which is the REST API used to communicate with the Docker daemon on the host. If we can reach this socket from within the container, using a simple curl for instance, we can instruct it to launch a privileged container and then gain root access to the host system. We begin by checking for docker.sock:

```
```bash
shell> curl --unix-socket /var/run/docker.sock http://localhost/images/json
curl: (7) Couldn't connect to server

shell> ls /var/run/docker.sock
ls: cannot access '/var/run/docker.sock': No such file or directory
shell> mount | grep docker

# docker.sock not found
```
```

No luck there. We then check the kernel's version, hoping for one that has some documented exploits to land on the host, but we strike out once more. The machine is running a 4.14.146 kernel, which at the time I ran this was only a couple of versions behind the latest version:

```
```bash
shell> uname -a
Linux f1a7a6f60915 4.14.146-119.123.amzn2.x86_64 #1
```
```

All in all, we are running as a relatively powerless root user inside an up-to-date machine without any obvious misconfigurations or exploits. We can always set up a similar kernel in a lab and then drill down into memory structures and syscalls until we find a zero-day to break namespace isolation, but let's leave that as a last resort kind of thing.

The first impulse of any sane person trapped in a cage is to try to break free. It's a noble sentiment. But if we can achieve our most devious goals while locked behind bars, why spend time sawing through them in the first place?

It sure would be great to land on the host and potentially inspect other containers, but given the current environment, I believe it's time we pull back from the barred window, drop the useless blunt shank, and focus instead on the bigger picture.