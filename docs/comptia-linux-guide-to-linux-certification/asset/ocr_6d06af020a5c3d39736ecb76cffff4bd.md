called research, you can run the following command to specify that the research subdirectory should be treated as a ZFS subfilesystem:

```
[root@server1 ~]# **zfs create datastorage4/research**
[root@server1 ~]# _
```

To see a list of ZFS file systems and subfilesystems that are available for ZFS management, you can run the **zfs list** command:

```
[root@server1 ~]# **zfs list**
NAME USED AVAIL REFER MOUNTPOINT
  datastorage4 286K 970M 42.6K /datastorage4
  datastorage4/research 38.6K 970M 38.6K /datastorage4/research
[root@server1 ~]# _
```

To list the specific configuration parameters that you can modify for the research subfilesystem, you can use the **zfs get all** command:

```
[root@server1 ~]# **zfs get all datastorage4/research | less**
NAME  PROPERTY  VALUE  SOURCE
datastorage4/research  type  filesystem  -
datastorage4/research  creation  Tue Sep 30 13:41 2015  -
datastorage4/research  used  38.6K  -
datastorage4/research  available  214M  -
datastorage4/research  referenced  38.6K  -
datastorage4/research  compressratio  1.00x  -
datastorage4/research  mounted  yes  -
datastorage4/research  quota  none  default
datastorage4/research  reservation  none  default
datastorage4/research  recordsize  128K  default
datastorage4/research  mountpoint  /datastorage4/research  default
datastorage4/research  sharenfs  off  default
datastorage4/research  checksum  on  default
datastorage4/research  compression  off  default
datastorage4/research  atime  on  default
datastorage4/research  async_write  on  default
datastorage4/research  devices  on  default
datastorage4/research  exec  on  default
datastorage4/research  setuid  on  default
datastorage4/research  readonly  off  default
:
```

You can modify the settings for the research subfilesystem to suit your needs. For example, to limit the total size of files within the research subfilesystem to 10GB, you could use the **zfs set quota=10G datastorage4/research** command, or to ensure that the contents of the research subfilesystem are read-only, you could run the **zfs set readonly=on datastorage4/research** command.

On Linux systems, ZFS volumes are mounted by the ZFS system and not via entries within the /etc/fstab file by default. As a result, to ensure that the datastorage1, datastorage2, data-storage3, and datastorage4 volumes created during the examples in this section are mounted