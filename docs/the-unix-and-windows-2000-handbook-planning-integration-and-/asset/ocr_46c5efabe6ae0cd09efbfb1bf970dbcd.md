+   2. Click Use Simple Mapping and then enter your NIS domain information or your PCNFSD server. This will map logins that are identical between your Windows domain and specified UNIX NIS domain. If your Windows and UNIX logins are different, you need to click Use Advanced Mapping.
+   3. The File Settings tab allows you to set read, write, and execute permissions for new files or folders created.
+   4. The Performance tab contains parameters for buffer sizes, timeouts, retries, and mount types. Go with the defaults on the performance page unless you experience problems.

> Don't forget to save your settings by clicking the disk in the upper right-hand corner of each configuration page.

Now you are ready to mount NFS filesystems. Mounting an NFS filesystem is accomplished in Windows Explorer following the same procedures for a Windows 2000 share. You can also mount NFS filesystems from the command line with the mount command. The mount command is located in the common folder under the Services for UNIX directory. The mount command is invoked with the following switches/parameters:

```
mount [switches] [network path] [drive] where
switches /u: username /o options Table8mount Valid only for that filesystem
network path = server://full/path/name or \\server\full\path\name
drive = drive: `
```

A mount command invoked without any switches or parameters displays all currently NFS-mounted filesystems on the local machine. The specific options are listed in Table 8.8.

| Table 8.8 Specific Options of the mount Command |
| Option | Definition |
| Rsize=n | Read buffer size in bytes. |
| Wsize=n | Write buffer size in bytes. |
| Timeo=n | NFS timeout in tenths of a second. |
| Retrans=n | NFS retransmissions; default is 5. |
| Soft | hard | Soft or hard mount. |