# 5.3 Network Applications

out of hard drives, it can also allow a user's home directory to exist any-where on the network, just as if it were local.

Setting up NFS for use is easy, as most Linux installations start up the necessary software at boot time. All that's left is to configure the NFS servers.

If NFS isnt not started on bootup, all you need to do is fire up rpc.mountd and rpc.nfsd on startup. This can be in the rc.local, or in a script in the /etc/rc3.d directory. The other item that needs to exist is the /etc/exports file list which directories can be exported to other machines.

The /etc/exports file has a setup of the following:

directory options

where directory is the directory to be exported, and options are any additional options to work on that. The options are many and can provide different options per host. Any option not enclosed in a host are assumed to be for any other hosts. Options can be of the:

+   * insecure—allow non-authenticated access.
* ro—read-only (good for use with insecure).
* rw—read-write.
* root_squash—prevents the root user from having any special access to the NFS directory by mapping UID 0 (root) to UID 65524. 11 This option is off by default
* no_root_squash—allows the root user to manipulate the partition as it is local. This is turned by default.
* all_squash—same as root_squash, but does it for all UIDs.
* no_all_squash—no UIDs are squashed.

Options can be prefaced with a hostname to apply that option to only that host.

```
/pub wayga(rw)
```

The way machine can mount the directory in read-write mode for all users (the default). The ro option means read-only.

```
/pub/foo wayga(noaccess)
```

> 11also known as the nobody user