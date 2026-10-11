# Disk Quotas

Solaris offers a disk quota system, as do other forms of Unix, which allows an administrator to set the amount of disk space that a user can store on a partition. The feature isn't often set up on a stand-alone workstation or even on a workstation on a network; it is applied in multiuser environments such as captive disks inside a server, on server-attached RAID systems, or on large storage arrays with Solaris server support. Using disk quotas is a very important tool in managing storage as a network asset because they can save a company money as well as prevent a rogue process such as a virus from completely filling up a partition and bringing a system to a halt or slowing a system down enough so that it is unusable.

In setting disk quotas, an administrator needs to know how much disk space is available for use, the number of users that space will support, and which volumes should have quotas applied to them. The specification uses a soft limit and a hard limit. With the soft limit, a warning is issued to a user when the user is close to exceeding the limit; with a hard limit, additional files may not be created until the user frees up disk space already consumed. In Solaris, when a user exceeds their soft limit, the system sends a specified number of error messages (as set by the system administrator) and then behaves as if the hard limit was reached.

The edquota command is used to define quotas inside the vi editor (unless you have another editor specified in your EDITOR environmental variable) and has the following syntax:

```
edquota <username>
```

As an example of setting a disk quota, do the following:

+   1. Log in as root. (Only a superuser can edit disk quotas, but any user can determine their quota settings and usage with the quota command for their particular username. A superuser can pass a list of usernames as the argument to the quota command to review settings and usage for two or more users.)

+   2. Enter vi /etc/vfstab at the command line, then add the rq flag to the mount options for the file system you wish to set the quota on.

+   3. Enter cd <directoryname> (change directory), where <directoryname> is the directory that serves as the mount point for the file system that will have the quota.

+   4. Create a file called quotas in that directory by entering the touch quotas command at the command line.

+   5. Enter chmod u+rw,go-rwx quotas to allow quotas to be read and written for the root user only.