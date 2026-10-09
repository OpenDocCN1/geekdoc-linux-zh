Check rpcbind is running  A new Fedora/RHEL system boots with `rpcbind` installed and running; For NFSv3 only (not NFSv4) `rpcbind` must be running before you can start the `nfs` service. Use the `systemctl status` command to make sure `rpcbind` is running.

```
# systemctl status rpcbind.service
```

# JUMPSTART I: MOUNTING A REMOTE DIRECTORY HIERARCHY

To set up an NFS client, mount the remote directory hierarchy the same way you mount a local directory hierarchy (page 520).

The following examples show two ways to mount a remote directory hierarchy, assuming `dog` is on the same network as the local system and is sharing `/home` and `/export` with the local system. The `/export` directory on `dog` holds two directory hierarchies you want to mount: `/export/progs` and `/export/oracle`. The example mounts `dog`'s `/home` directory on `/dog.home` on the local system, `/export/progs` on `/apps`, and `/export/oracle` on `/oracle`.

First run `mkdir` on the local (client) system to create the directories that are the mount points for the remote directory hierarchies:

```
# mkdir /dog.home /apps /oracle
```

You can mount any directory hierarchy from an exported directory hierarchy. In this example, `dog` exports `/export` and the local system mounts `/export/progs` and `/export/oracle`. The following commands manually mount the directory hierarchies one time:

```
# mount dog:/home /dog.home
# mount -o ro,nosuid dog:/export/progs /apps
# mount -o ro dog:/export/oracle /oracle
```

By default, directory hierarchies are mounted read-write, assuming the NFS server is exporting them with read-write permissions. The first of the preceding commands mounts the `/home` directory hierarchy from `dog` on the local directory `/dog.home`. The second and third commands use the `-o ro` option to force a read-only mount. The second command adds the `nosuid` option, which forces `setuid` (page 196) executables in the mounted directory hierarchy to run with regular permissions on the local system.

nosuid option  If a user has the ability to run a `setuid` program, that user has the power of a user with `root` privileges. This ability should be limited. Unless you know a user will need to run a program with `setuid` permissions from a mounted directory hierarchy, always mount a directory hierarchy with the `nosuid` option. For example, you would need to mount a directory hierarchy with `setuid` privileges when the root partition of a diskless workstation is mounted using NFS.

nodev option  Mounting a device file creates another potential security hole. Although the best policy is not to mount untrustworthy directory hierarchies, it is not always possible to