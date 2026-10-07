# Table 12-10 Summary of File System Features (Continued)

| Feature | UFS | VxFS | QFS | Notes |
|---|---|---|---|---|n| Separate log | Yes, with SDS | Yes with NFS Acc. | No | A separate log device can be attached to the file system to avoid seeking backward and forward from the log to the data. |
| Extended band | No | Yes | Yes | Fewer disk seeks due to simpler block allocation schemes. |
| Direct I/O | Yes, 2.6 | Yes | Yes | Direct I/O options allow bypassing of the page cache based on mount options and runtime directives. |
| Expandable | Yes | Yes | No | The file system size can be expanded online. |
| Shrinkable | No | Yes | No | The file system size can be shrunk online. |
| Snapshot, by locking file system | Yes | Yes | No | The file system can be locked and frozen for a backup snapshot. Locking suspends all file system activity during the backup. |
| Online snapshot | No | Yes | No | A frozen version of the file system can be mounted while the main file system is online. This version can be used for online backup. |
| Quotas ACLs | Yes | Yes | No | Disk space quotas can be enforced. Enhanced file permissions via Access Control Lists. |
| HSM capable | No | Yes | Yes | Automatic hierarchical storage management options. |
| Page cache friendly | Yes | No | Yes | UFS will not cause memory shortage when used in sequential mode. VxFS must be used in direct or sequential advise to avoid causing a memory. |
| Stripe alignment | No | Yes | Yes | Ability to align clustered writes with storage stripe to allow whole stripe writes. Provides superior RAID-5 performance. |
| Integrated Volume Manager | No | No | Yes | Striping and concatenation across multiple storage devices possible from file system. |