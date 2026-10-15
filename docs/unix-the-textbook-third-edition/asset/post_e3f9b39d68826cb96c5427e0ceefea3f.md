
options=9b<RXCSUM,TXCSUM,VLAN_MTU,VLAN_HWtagging,
VLAN_HWCSUM>
ether 08:00:27:38:ba:74
inet 192.168.0.100 netmask 0xffffffff broadcast
192.168.0.100
media: Ethernet autoselect (1000baseT <full-duplex>)
status: active
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> metric 0 mtu 16384
        options=600003<RXCSUM,TXCSUM,RXCSUM_IPV6,TXCSUM_IPV6>
root@44599667-9574-11e5-9cc9-08002738ba74:~ #

Change the root password in the jail bobsecond while we are logged into its console:

```
root@44599667-9574-11e5-9cc9-08002738ba74:~ # passwd
Changing local password for root
New Password: xxxxx
Retype New Password: xxxxx
root@44599667-9574-11e5-9cc9-08002738ba74:~ #
```

To close the console connection into bobsecond, type exit or logout.

Restarting and stopping a jail:

```
[bob@pcbsd-1233] /usr/home/bob# iocage restart bobsecond
* Soft restarting 44599667-9574-11e5-9cc9-08002738ba74
(bobsecond)
[bob@pcbsd-1233] /usr/home/bob#
[bob@pcbsd-1233] /usr/home/bob# iocage stop bobsecond
* Stopping 44599667-9574-11e5-9cc9-08002738ba74 (bobsecond)
+ Running pre-stop      OK
+ Stopping services     OK
+ Removing jail process OK
+ Running post-stop     OK
rctl: RACCT/RCTL present, but disabled; enable using kern.
racct.enable=1 tunable
[bob@pcbsd-1233] /usr/home/bob#
```

Destroying a jail:

If you wish to remove a jail from a system, you destroy it.
You also have to make sure the jail is stopped, or down!

First use iocage list to see what jails we have defined:

```
[bob@pcbsd-1233] /usr/home/bob# iocage list
```

JID | UUID | BOOT | STATE | TAG
--- | --- | --- | --- | ---
2 | 44599667-9574-11e5-9cc9-08002738ba74 | off | up | bobsecond
- | 527c21ff-9573-11e5-9cc9-08002738ba74 | off | down | 2015-11-27@17:57:04

Then use iocage destroy to completely remove the first jail we created:

```
[bob@pcbsd-1233] /usr/home/bob# iocage destroy
2015-11-27@17:57:04
WARNING: this will destroy jail 527c21ff-9573-11e5-9cc9-08002738ba74
Dataset: tank/iocage/jails/527c21ff-9573-11e5-9cc9-08002738ba74
Are you sure ? y[N]: y
Destroying: 527c21ff-9573-11e5-9cc9-08002738ba74
[bob@pcbsd-1233] /usr/home/bob#
```

Notice that in the iocage destroy command, we used the tag of the first jail as its identifier.

## EXERCISE 25.4

Create a jail, start it, and set properties on it so you can ssh into it from the host, and from other computers on your local area network (LAN).

## 25.3 SOLARIS ZONES VIRTUALIZATION METHOD

Solaris zones are used to virtualize OS services and provide an isolated and secure environment for running applications. A nonglobal zone, usually called just a zone, is a virtualized OS environment created within a single instance of the Solaris OS. The single instance of the OS is called the global zone. The global and any nonglobal zones share only one instance of the Solaris kernel.

### 25.3.1 Nonglobal Zone State Model

Before doing some example installations of zones, it is important to know what operating states a nonglobal zone can have. The following model details those states, as seen in Figure 25.1. Example commands that affect those states are also shown in the description of the model that follows:

A nonglobal zone can be in one of the following seven states, as shown in Figure 25.1:

Configured: The zone's configuration is complete and committed to stable storage. However, those elements of the zone's application environment that must be specified after initial boot are not yet present.

Incomplete: During an install or uninstall operation, zoneadm sets the state of the target zone to incomplete. On successful completion of the operation, the state is set to the correct state.

![](img/02e070097d401d3bf7de4bf1c470b267_1306_0.png)

## FIGURE 25.1 Nonglobal zone states.

A damaged installed zone can be marked incomplete by using the mark subcommand of zoneadm. Zones in the incomplete state are shown in the output of zoneadm list -iv.

Unavailable: Indicates that the zone has been installed, but cannot be verified, made ready, booted, attached, or moved. A zone enters the unavailable state at the following times:

- When the zone’s storage is unavailable and svc:/system/zones:default begins, such as during system boot
- When the zone’s storage is unavailable
- When archive-based installations fail after successful archive extraction
- When the zone’s software is incompatible with the global zone’s software, such as after an improper -F (force) attach

Installed: The zone’s configuration is instantiated on the system. The zoneadm command is used to verify that the configuration can be successfully used on the designated Solaris system. Packages are installed under the zone’s root path. In this state, the zone has no associated virtual platform.

Ready: The virtual platform for the zone is established. The kernel creates the zsched process, network interfaces are set up and made available to the zone, file systems are mounted, and devices are configured. A unique zone ID is assigned by the system. At this stage, no processes associated with the zone have been started.

Running: User processes associated with the zone application environment are running. The zone enters the running state as soon as the first user process associated with the application environment (init) is created.
