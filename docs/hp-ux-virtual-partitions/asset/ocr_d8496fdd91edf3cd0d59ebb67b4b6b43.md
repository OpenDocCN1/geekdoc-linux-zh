```
-rwxr-xr-x 1 root sys 23184584 Aug 4 12:22 vmlinux.prev
#
```

Notice that among the directories shown are two related to Dynamically Loadable Kernel Modules (DLKMs.) These are kernel modules that can be included in the kernel without having to reboot the system.

In order to make a change to the kernel, we would change to the /stand/build directory, where all work in creating a new kernel is performed, and issue the system_prep command as shown below:

```
# cd /stand/build
# /usr/lib/sysadm/system_prep -s system
```

We can now proceed to make the desired changes to the kernel, including adding a driver or subsystem such as cdfs for a CD-ROM file system. With the dynamically loadable kernel module (DLM) structure in place with 1.1i, we must use knsystem and knptune to make changes in the kernel system and system description files.

You can use knmute to view the value and parameters related to existing kernel parameters as well as to make proposed modifications to the kernel. The following listing shows issuing knmute (without the -i option to view details) to view a summary of the currently running kernel:

```
# knmute
```

| Parameter | Current | Dyn Planned | Module | Version |
|:---|:---|:---|:---|:---|
| NTRLBLKSIGNED | 2 | - | - | - |
| NSTREVENT | 50 | - | 50 | |
| NSTREPGNH | 16 | - | 16 | |
| NSTRCHRGH | 0 | - | 0 | |
| STRCTLRSZ | 1024 | - | 1024 | |
| STRMSGSZ | 65535 | - | 65535 | |
| acct_resume | 4 | - | 4 | |
| acct_suspends | 2 | - | 2 | |
| aio_listio_max | 256 | - | 256 | |
| aio_max_od| 2048 | - | 2048 | |
| aio_physmem_pct | 10 | - | 10 | |
| aio_prio_delta_max | 20 | - | 20 | |
| allocate_fs_swamap | 0 | - | 0 | |
| alwaysdump | 1 | - | 1 | |
| bootapplink|de | - | 256 | |
| bufcache_hash_locks | 128 | - | 128 | |
| bufpages | 0 | - | 0 | |