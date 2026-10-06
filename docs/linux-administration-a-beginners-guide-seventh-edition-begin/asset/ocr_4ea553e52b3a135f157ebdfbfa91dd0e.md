# CHAPTER 23 Network File System (NFS)

617

> > [!NOTE]\ 
> There is one exception to the preferred arrangement of having a soft mount with a retrans=r value specified: Don't use this arrangement when you have data that must be committed to disk no matter what and you don't want to return control to the application after the data has been committed. (NFS-mounted mail directories are typically mounted this way.)

# Cross-mounting Disks

Cross-mounting can be described as the process of having serverA NFS-mounting serverB's disks and serverB NFS-mounting serverA's disks. Although this may appear innocuous at first, there is a subtle danger in doing this. If both servers crash, and each server requires mounting the other's disk in order to boot, you've got a chicken and egg problem. Server won't boot until serverB is booting, but

To avoid this problem, make sure you don't get yourself into a situation where this happens. Ideally, all of your servers should be able to boot completely without needing anyone else's disks for anything. However, this doesn't mean you can't cross-mount at all. There are legitimate reasons for needing to make home directories available across all servers.

In these situations, you may set your /etc/fstab entries to use the bg process. By doing, you will allow each server to background the mount process for failed mounts, giving all of the servers a chance to boot completely and then properly make their NFS-mountable file systems available.

# The Importance of the intr Option

When a process makes a system call, the kernel takes over the action. During the time that the kernel is handling the system call, the process may not have control over itself. In the event of a kernel access error, the process must continue to wait until the kernel return requests; the process can't give up and quit. In normal cases, the kernel's control isn't a problem, because, kernel requests get resolved quickly. When there's an error, it can be a nuisance. Because of this, NFS has an option to mount file systems with the interruptible flag (the intr option), which allows a process that is waiting on an NFS request to give up and move on.

In general you have reason not to use the intr option, it is usually a good idea to do so.

# Performance Tuning

The default block size that is transmitted with NFS version 3 is 8192 bytes (for NFS4, it is 32,768 bytes). There might be situations where you need to tune these default values to take advantage of faster network stacks or faster equipment available to you. This is where the wsize (write size) and rsize (read size) options come in handy. You will usually want to tune these values up or down (in cases where you have older hardware) to suit your deployment environment.