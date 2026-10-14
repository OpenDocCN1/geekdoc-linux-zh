
## 13.9.4 Adjusting CFS Memory Usage

If you have an application that is reporting an EMFILE error, "too many open files", you might be experiencing one of two memory-related problems:

- 1. The member is out of vnodes.
- 2. The CFS server has reached svrcfstok_max_percent.

### 13.9.4.1 Is the CFS Client Out of vnodes?

To see if the CFS client is out of vnodes, you can use your favorite kernel debugger and get the value for the global variables total_vnodes and free_vnodes. Then get the value of the max_vnodes attribute in the vfs subsystem using the sysconfig(8) command.

If total_vnodes is equal to vfs:max_vnodes and free_vnodes is equal to zero, then you should increase the vfs:max_vnodes value.

We wrote a Perl script to get the values and do the math so we wouldn't have to remember the rules or variable names.

```
# ./vnode
If the total (in-use) vnodes is equal to vfs:max_vnodes and
the free vnodes is equal to zero, then increase vfs:max_vnodes
vnodes in-use    vfs:max_vnodes    AND    free vnodes = zero
-------------    -------------    ------    -------------
6129         <      18699            2706
This member has available vnodes.
Verify that the CFS server has not exceeded cfs:svrcfstok_max_percent
```

Using the manual approach:

```
# sysconfig -q vfs max_vnodes
vfs:
max_vnodes = 18699
```

### vfs:max_vnodes attribute values

| Minimum Value | Maximum Value | Default Value |  |
|---|---|---|---|
| 0 | 1717986918 | 1000 | If system main memory is 24MB or less |
|  |  | Number of vnodes that can be contained in 5% of the system's main memory. | If system main memory is greater than 24MB |

Table 13-3: max_vnodes attribute values

# NOTE:

The max_vnodes variable is a kernel global variable as well and can also be obtained from the kernel debugger.

The max_vnodes attribute can be reconfigured dynamically using the sysconfig command.

```
# sysconfig -r vfs max_vnodes=50000
```

The minimum, maximum, and default values of the max_vnodes attribute are shown in Table 13-3.

If the CFS client has not exceeded max_vnodes and still has free vnodes available, then you should check to see if the CFS server has reached svrcfstok_max_percent.

### 13.9.4.2 Has the CFS Server Reached svrcfstok_max_percent?

The CFS server must keep track of all vnodes that are cached on CFS clients – this requires approximately 1600 bytes of system memory for data structures (a token structure, AdvFS access structures, vnode structures, etc.) per cached vnode. The CFS server can use up to cfs:svrcfstok_max_percent of main memory to hold these data structures. The default for the svrcfstok_max_percent attribute is 25% but can be set from 5% to 50%.

As of this writing, in order to see if the CFS server has reached svrcfstok_max_percent, you need to use a kernel debugger to scope out the values of the svrtok_active_svrcfstok and cfs_max_svrcfstok kernel global variables.

```
# print 'printf "svrtok_active_svrfctok = %d, \\n"',
> cfs_max_svrfctok = %d, svrtok_active_svrfctok;
> quit ; | dbx -k /vmunix 2> /dev/null | tail -1
svrtok_active_svrfctok = 4608, cfs_max_svrfctok = 76833
```

If svrtok_active_svrfctok is greater than or equal to cfs_max_svrfctok, then you can try one or more of the following suggestions to get your file systems up and running again:

- 1. Use the `cfsfsngr(8)` command to relocate some file systems to another cluster member. See section 13.9.1.1 for more information.
- 
- 2. Increase the value of the kernel global variable `cfs_max_svrfctok` using your favorite kernel debugger.

```
# dbx -k /vmunix

(dbx) assign cfs_max_svrfctok=92500
92500
(dbx) pd cfs_max_svrfctok
92500
(dbx) quit
```

- 3. Increase the value of `cfs:svrfctok_max_percent` in `/etc/sysconfigtab` using the `sysconfigdb(8)` or `dxkerneltuner(8)` command and then reboot the member.

# NOTE:

Never ones to shy away from a challenge, we wrote a script called `cfssvrtok` that checks the values of `svrtok_active_svrfctok` and `cfs_max_svrfctok` and then offers to modify `cfs_max_svrfctok` for you.

### 13.9.4.3 The CFS Server is Running Out of Memory?

If a member acting as a CFS server does not have a large amount of memory, you may want to consider setting the `cfs:svrcfstok_max_percent` attribute’s value to something lower than the 25% default. We do not recommend you do this unless you find that the member is consistently running out of memory and you cannot add additional memory.
