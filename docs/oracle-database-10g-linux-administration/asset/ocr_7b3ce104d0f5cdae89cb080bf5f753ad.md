# Oracleasm Optional Parameters

The Oracle ASM library driver supports a number of optional commands that are useful for administering ASM. You should be familiar with these commands if you intend to use ASM:

| Command | Description |
| --- | --- |
| /etc/init.d/oracleasm configure | Used to configure the ASM module and ASM configuration file as well as set up the ASM mount point. |
| /etc/init.d/oracleasm [enable/disable] | These commands will change whether the ASM library driver starts on system boot. This command modifies the /etc/sysconfig/oracleasm file. |
| /etc/init.d/oracleasm [start/stop/restart] | These commands will stop, start, or restart the ASM library driver. |
| /etc/init.d/oracleasm status | Displays the status of the ASM library driver. |
| /etc/init.d/oracleasm createdisk name dev | This command takes the name of the volume to be created and a device name in order to associate a disk drive with ASM: /etc/init.d/oracleasm createdisk VOL1 /dev/sda3. |
| /etc/init.d/oracleasm deletedisk name | Removes a disk drive from its association with ASM. |
| /etc/init.d/oracleasm listdisks | Lists all of the disk names associated with ASM. |
| /etc/init.d/oracleasm querydisk [name/dev] | Used to determine if a disk name or disk device is associated with ASM. See the example that follows. |
| /etc/init.d/oracleasm scandisks | Used in RAC clusters in order to enable the cluster nodes to identify which disks have been associated with ASM on another node. |

Here are a few examples of using the /etc/init.d/oracleasm commands:
Checking the status of the ASM library driver:

```
[root@ptc6 root]# /etc/init.d/oracleasm status
Checking if ASM is loaded: [ OK ]
Checking if /dev/oracleasm is mounted: [ OK ]
Restarting the ASM library driver:
```

```
[root@ptc6 root]# /etc/init.d/oracleasm restart
Unmounting ASMLib driver filesystem [ OK ]
Unloading module "oracleasm" [ OK ]
Loading module "oracleasm" [ OK ]
```