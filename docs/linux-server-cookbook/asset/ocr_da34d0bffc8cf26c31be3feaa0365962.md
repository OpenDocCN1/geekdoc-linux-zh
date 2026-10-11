```
Using Catalog "MyCatalog"
Run Restore job
JobName: RestoreFiles
Bootstrap: /opt/bacula/working/bacula-dir.restore.3.bsr
Where: /opt/bacula/archive/bacula-restores
Replace: Always
FileSet: Full Set
Backup Client: rhel-fd
Restore Client: rhel-fd
Storage: bacula-sd
When: 2022-11-12 20:27:37
Catalog: MyCatalog
Priority: 10
Plugin Options: *None*
OK to run? (yes/mod/no): yes
Job queued. JobId=14
```

*Figure 14.11: Example restoring files with the command bconsole*

When the **Jobs** finishes, and if there is no error, the files are available. *Figure 14.12* shows the content of the directory indicated before:

```
[root@rhel ~]# tree /opt/bacula/archive/bacula-restores/
/opt/bacula/archive/bacula-restores/
└── etc
   ├── resolv.conf
   └── services
1 directory, 2 files
```

*Figure 14.12: Example listing restored files in the client*

# ## Relax-and-Recover (RearR)

This software is an open-source *bare metal* disaster recovery solution. It is easy to install, configure and use for restoring systems. This solution generates a copy of the system ready to be used. It supports various boot media (*ISO, PXE, USB, or eSATA*) and a variety of network protocols (*nfs, cifs, ftp, or http*) as well as different Backup strategies (*Symantec Netbackup, EMC Networker*, among others).