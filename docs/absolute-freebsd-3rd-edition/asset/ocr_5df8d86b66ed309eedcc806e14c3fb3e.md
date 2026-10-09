however, and then restore it after applying patches. But when you’re first learning, don’t get fancy. Get a basic userland working first.

# The NFS Server and the Diskless Client Userland

Many tutorials on diskless operation suggest using the server’s userland and root partition for diskless clients. That might be easy to do, but it’s not even vaguely secure. Your diskless server probably has programs on it that you don’t want the clients to have access to, and it certainly has sensitive security information that you don’t want to hand out to a whole bunch of workstations. Providing a separate userland is a much wiser option.

While you can provide a separate userland in many ways, I find that the simplest is to slightly modify the jail(8) construction process from Chapter 22. First, make a dataset, UFS filesystem, or directory for our diskless clients to use as their root directory, and then install a userland and kernel in that directory. Extract the `base.txz` and `kernel.txz` distribution files for the version of FreeBSD in that directory.

```
# tar -xpf base.txz -C /diskless/1/
# tar -xpf kernel.txz -C /diskless/1/
```

If you’ve built a FreeBSD you want to run, that works too. Here, we install a locally built userland in /diskless/1:

```
# cd /usr/src
# make installworld DESTDIR=/diskless/1
# make installkernel DESTDIR=/diskless/1
# make distribution DESTDIR=/diskless/1
```

Now tell your NFS server about this directory. I intend to install several diskless systems on this network, so I offer this directory via NFS to my entire subnet. The clients don’t need write access to the NFS root, so I export it read-only. The following /etc/exports line does this:

```
/diskless/1 -ro -maproot=0 -alldirs -network 198.51.100.0 -mask 255.255.255.0
```