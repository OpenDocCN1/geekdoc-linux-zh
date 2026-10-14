
2. Modify the application.tdf file.

The following entries should be added to the file.

```
####################
attribute: USR_CFS
type: name_list
switch: -o cfs
default:
required: no
```

```
####################
attribute: USR_MNT_PT
type: name_list
switch: -o mp
default:
required: no
```

## 24.4.1.2 Creating a CFS Server Action Script

As mentioned in section 24.4.1, the “start” and “check” entry points to the action script should be modified to check the location of the CFS server for the list of file systems and relocate the CFS server if the member running the application resource is not the CFS server.

The following tasks will need to be added to the action script:

- Check to see if the file system is mounted.
  - If the file system is not mounted, either mount it or post a message and exit.
  - If the file system is mounted privately, exit because either the member mounted it so it is the CFS server, or the member did not mount it in which case it cannot be unmounted or relocated by the member.

The following piece of code (written in Korn shell) is one approach to checking the file system status.

```
ic=0
jc=0
for i in $USR_CFS
do
    (( ic += 1 ))
    for j in $USR_MNT_PT
    do
        (( jc += 1 ))
        if (( $ic != $jc ))
        then
            continue
        fi
        fs=$(mount | grep $i" )" , stat=$?
```

Loop through the list of file systems.

Loop through the list of mount points.

Make sure the file system and mount point is the same place in the list.

See if the file system is mounted.

- If the relocation fails, should another attempt be made? If so, how many? When should you give up and return an error?

There is not just one answer to each of these questions. Use your best judgment and try a few options to see what works best for your configuration.

## 24.4.1.3 Creating a CFS Server Application Resource

In this section, we will create a CFS Server application resource that we'll name cfs_common. The cfs_common resource will be a "favored" resource and used to relocate the CFS server duties for cluster_root, cluster_usr, and cluster_var to member1 (molari). Of course this resource (or a similar one) can be used as a dependency for another application resource.

We will use the caa_profile command with the following options:

- -a - Our customized CFS server script.
- -o cfs - Used to set the USR_CFS attribute variable.
- -o mp - Used to set the USR_MNT_PT attribute variable.
- -o as - Set AUTO_START.
- -o ap - Set ACTIVE_PLACEMENT.
- -p - Set the PLACEMENT to "favored".
- -h - Set the HOSTING_MEMBER.

```
# caa_profile -create cfs_common -t application -a cfs_relo.scr \
> -o cfs="cluster_root#root cluster_usr#usr cluster_var#var",\
> mp="/ /usr /var",as=1,ap=1 -p favored -h molari
```

Verify the resource profile with the caa_profile command with the "-print" option.

```
# caa_profile -print cfs_common
NAME=cfs_common
TYPE=application
ACTION_SCRIPT=cfs_relo.scr
ACTIVE_PLACEMENT=1
AUTO_START=1
CHECK_INTERVAL=60
DESCRIPTION=cfs_common
FAILOVER_DELAY=0
FAILURE_INTERVAL=0
FAILURE_THRESHOLD=0
HOSTING_MEMBERS=molari
OPTIONAL_RESOURCES=
PLACEMENT=favored
REQUIRED_RESOURCES=
RESTART_ATTEMPTS=1
SCRIPT_TIMEOUT=60
USR_CFS=cluster_root#root cluster_usr#usr cluster_var#var
USR_MNT_PT=/ /usr /var
```

## 24.4.2 Relocating a CFS Server from an Application Resource

Instead of having a separate resource for relocating file systems to a different CFS server, you can add logic to your application resource’s action script to do the relocation(s).

You will need to modify your “start” and “check” entry points.

- Verify that the file system is mounted. If it is unmounted, should you mount it or fail to start the resource?
- Locate the CFS server for the file system.
  - If the member is the CFS server, no relocation is necessary.
  - If the CFS server is not the member, then relocate the CFS server.
- If the relocation was successful, start the application.
- If the relocation was unsuccessful, do you try again?
  - If so, you must determine how many times to attempt to relocate the domain.
  - You must also decide what action to take if you cannot relocate the domain.
    - Should the resource start anyway? Probably. Your users will still be more efficient using an application that is accessing its data across the cluster interconnect than not being able to use the application at all.

## 24.5 Private Storage Resource

With the advent of the CFS, all file systems are available to all cluster members. For normal cluster operations, this is probably what you want. However, what if you have data that you want to restrict to one member?

*TruCluster Server* supports the notion of privately mounted file systems (also know as partitioned file systems -- see Chapter 13, section 13.4³). A partitioned file system is mounted and accessible by one cluster member.

Why would you want a partitioned file system resource? If you have an application resource that uses data, which you do not want any other cluster member to be able to access, then a partitioned file system may be the solution. If you have application data that is on a UFS file system and you would like the file system to be mounted read-write⁴ as well as have the file system highly available,

³ Partitioned file systems were not supported in V5.0A.

⁴ Read-write UFS support began in *TruCluster Server* version 5.1A but is restricted to a partitioned file system
