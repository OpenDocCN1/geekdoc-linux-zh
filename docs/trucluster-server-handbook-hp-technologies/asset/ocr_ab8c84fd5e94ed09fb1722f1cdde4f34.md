# System Administration Tasks

| Task | Cluster-Wide | Member-Specific | Chapter or Section | Notes |
|---|---:|---:|---|---|
| Accounting | × | ✓ | 19 | Enable on a specific host. `rcmgr -h 3 set ACCOUNTING YES`<br>Enable cluster-wide. `rcmgr -c set ACCOUNTING YES` |
| Auditing | ✓ | × | 19.4.4.1 | Cluster-wide Configuration, Member-Specific Audit Logs. |
| Backups | ✓ | × | 22 | CDSLS are normal symbolic links. |
| Cron | × | ✓ | 21 | `/usr/spool/cron` is a CDSL |
| Dumps | × | ✓ | A | Use dumpsys to force dumps on each member. |
| EVM Events | ✓ | ✓ | 8, 12 | `cluster_event` attribute forces posting to all members |
| File Systems | ✓ | ✓ | 6, 13 | CFS allows cluster-wide file systems |
| Kernel Builds | × | ✓ | 12 | Kernel configuration files are located in `cluster_usr`, and can be built on any member, but the kernel itself is member-specific. |
| Licensing | × | ✓ | 4, 5, 10, 11 | Every cluster member must be individually licensed. |
| Loading Software | ✓ | × | 10, 19 | Installed once, supported by CAA |
| LSM | ✓ | ✓ | 14 | Cannot be used for member boot partition |
| Non-Storage Devices | × | ✓ | 19 | Member-specific |
| O/S Install/Updates | ✓ | × | 5, 11, 19, 26 | Rolling Upgrade Supported |
| Performance | ✓ | ✓ | 19, 21, A | Cluster-Wide for Cluster Services, Member-Specific for Local Services |
| Printing | ✓ | × | 19.4.3 | New "on" `printcap` attribute |
| Processes and Scheduling | × | ✓ | 6, 19.2.4 | PIDs cluster-wide, Scheduling member-specific |
| Shutdown | ✓ | ✓ | 19.2.2 | Cluster-wide shutdown is supported |
| Startup | × | ✓ | 17 | Member-specific startup files |
| Storage Devices | ✓ | × | 7, 12, 15 | Supported through DRD and CFS |
| System Time | × | ✓ | 20 | Must be Synchronized |
| User Accounts | ✓ | × | 19.3.1 | The password and group files are cluster-wide |

**Table 19-1: System Administration Tasks**

# Chapter 19