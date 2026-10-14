we think it is easier and less risky to simply issue the **volencap** and **volreconfig** commands on each member as follows:

```
```shell
[host1]
#/usr/sbin/volencap swap / /sbin/volreconfig
```
```

```
```shell
[host2]
# rah sheridan-acs0 "/usr/sbin/volencap swap / /sbin/volreconfig"
```
```

Finish the encapsulation process by rebooting each member one at a time.

For additional information, see the *TruCluster Server Cluster Administration Guide* and the **volencap(8)** reference page.

# 14.7.3  Unencapsulation

There is no volunencap command, so the only way to unencapsulate a previously encapsulated disk, disk partition, or AdvFS domain is the hard way.

# 14.7.3.1  Unencapsulating an AdvFS Domain

In section 14.7.2.1 we encapsulated our **tcrhb** domain. In this section we’ll remove the domain from LSM.

To remove an encapsulated AdvFS domain from LSM, follow these steps:

+   1. Unmount the file systems.
+   2. Stop the volume(s).

```
```shell
# volstop vol-dsk6c
```
```

+   3. Remove the volume(s).

```
```shell
# voledit -rf rm vol-dsk6c
```
```

+   4. Remove the disk from the disk group.

```
```shell
# voldisk list | grep dsk6c
dsk6c     noprive     dsk6c0-AdvFS  rootdg     online
```
```