
string **accounts, net rpc rights** list returns a list of all privileged accounts on the server and the assigned rights.

**grant <user> <right [right ...]>** When called with no arguments, this function is used to assign a list of rights to a specified user or group. For example, to grant the members of the Domain Admins group on a Samba domain controller, the capability to add client machines to the domain, one would run:

```
root# net -S server -U domainin rpc rights grant \
        'DOMAIN\\Domain Admins' SeMachineAccountPrivilege
```

The following syntax has the same result:

```
root# net rpc rights grant 'DOMAIN\\Domain Admins' \
        SeMachineAccountPrivilege -S server -U domainin
```

More than one privilege can be assigned by specifying a list of rights separated by spaces. The parameter 'Domain\\Domain Admins' must be quoted with single ticks or using double-quotes to prevent the backslash and the space from being interpreted by the system shell.

**revoke <user> <right [right ...]>** This command is similar in format to **net rpc rights grant**. Its effect is to remove an assigned right (or list of rights) from a user or group.

> ### NOTE
>
> You must be connected as a member of the Domain Admins group to be able to grant or revoke privileges assigned to an account. This capability is inherent to the Domain Admins group and is not configurable.

By default, no privileges are initially assigned to any account because certain actions will be performed as root once smbd determines that a user has the necessary rights. For example, when joining a client to a Windows domain, **add machine script** must be executed with superuser rights in most cases. For this reason, you should be very careful about handing out privileges to accounts.

Access as the **root** user (UID=0) bypasses all privilege checks.

### 14.1.2 Description of Privileges

The privileges that have been implemented in Samba-3.0.11 are shown below. It is possible, and likely, that additional privileges may be implemented in later releases of Samba. It is also likely that any privileges currently implemented but not used may be removed from future releases as a housekeeping matter, so it is important that the successful as well as unsuccessful use of these facilities should be reported on the Samba mailing lists.

- SeAddUsersPrivilege This right determines whether or not smbd will allow the user to create new user or group accounts via such tools as net rpc user add or NT4 User Manager for Domains.

- SeDiskOperatorPrivilege Accounts that possess this right will be able to execute scripts defined by the add/ delete/ change share command in smb.conf file as root. Such users will also be able to modify the ACL associated with file shares on the Samba server.

- SeMachineAccountPrivilege This right controls whether or not the user can join client machines to a Samba-controlled domain.

- SePrintOperatorPrivilege This privilege operates identically to the printer admin option in the smb.conf file (see section 5 man page for smb.conf) except that it is a global right (not on a per-printer basis). Eventually the smb.conf option will be de-pre-cated and administrative rights to printers will be controlled exclusively by this right and the security descriptor associated with the printer object in the ntprinters.tdb file.

- SeRemoteShutdownPrivilege Samba provides two hooks for shutting down or rebooting the server and for aborting a previously issued shutdown command. Since this is an operation normally limited by the operating system to the root user, an account must possess this right to be able to execute either of these hooks.

- SeTakeOwnershipPrivilege This right permits users to take ownership of files and directories.

### 14.1.3 Privileges Supported by Windows 2000 Domain Controllers

For reference purposes, a Windows NT4 Primary Domain Controller reports support for the following privileges:

| Privilege | Description |
| :--- | :--- |
| SeCreateTokenPrivilege | Create a token object |
| SeAssignPrimaryTokenPrivilege | Replace a process level token |
| SeLockMemoryPrivilege | Lock pages in memory |
| SeIncreaseQuotaPrivilege | Increase quotas |
| SeMachineAccountPrivilege | Add workstations to domain |
| SeTcbPrivilege | Act as part of the operating system |
| SeSecurityPrivilege | Manage auditing and security log |
| SeTakeOwnershipPrivilege | Take ownership of files or other objects |
| SeLoadDriverPrivilege | Load and unload device drivers |
| SeSystemProfilePrivilege | Profile system performance |
| SeSystemtimePrivilege | Change the system time |
| SeProfileSingleProcessPrivilege | Profile single process |
| SeIncreaseBasePriorityPrivilege | Increase scheduling priority |
| SeCreatePagefilePrivilege | Create a pagefile |
| SeCreatePermanentPrivilege | Create permanent shared objects |
| SeBackupPrivilege | Back up files and directories |
| SeRestorePrivilege | Restore files and directories |
| SeShutdownPrivilege | Shut down the system |
| SeDebugPrivilege | Debug programs |
| SeAuditPrivilege | Generate security audits |
| SeSystemEnvironmentPrivilege | Modify firmware environment values |
| SeChangeNotifyPrivilege | Bypass traverse checking |
| SeRemoteShutdownPrivilege | Force shutdown from a remote system |

And Windows 200x/XP Domain Controllers and workstations reports to support the following privileges:

| Privilege | Description |
| :--- | :--- |
| SeCreateTokenPrivilege | Create a token object |
| SeAssignPrimaryTokenPrivilege | Replace a process level token |
| SeLockMemoryPrivilege | Lock pages in memory |
| SeIncreaseQuotaPrivilege | Increase quotas |
| SeMachineAccountPrivilege | Add workstations to domain |
| SeTcbPrivilege | Act as part of the operating system |
| SeSecurityPrivilege | Manage auditing and security log |
| SeTakeOwnershipPrivilege | Take ownership of files or other objects |
| SeLoadDriverPrivilege | Load and unload device drivers |
| SeSystemProfilePrivilege | Profile system performance |
| SeSystemtimePrivilege | Change the system time |
| SeProfileSingleProcessPrivilege | Profile single process |
| SeIncreaseBasePriorityPrivilege | Increase scheduling priority |
| SeCreatePagefilePrivilege | Create a pagefile |
| SeCreatePermanentPrivilege | Create permanent shared objects |
| SeBackupPrivilege | Back up files and directories |
| SeRestorePrivilege | Restore files and directories |
| SeShutdownPrivilege | Shut down the system |
| SeDebugPrivilege | Debug programs |
| SeAuditPrivilege | Generate security audits |
| SeSystemEnvironmentPrivilege | Modify firmware environment values |
| SeChangeNotifyPrivilege | Bypass traverse checking |
| SeRemoteShutdownPrivilege | Force shutdown from a remote system |
| SeUnDclockPrivilege | Remove computer from docking station |
| SeSyncAgentPrivilege | Synchronize directory service data |
| SeEnableDelegationPrivilege | Enable computer and user accounts to be trusted for delegation |
| SeManageVolumePrivilege | Perform volume maintenance tasks |
| SeImpersonatePrivilege | Impersonate a client after authentication |
| SeCreateGlobalPrivilege | Create global objects |

The Samba Team is implementing only those privileges that are logical and useful in the UNIX/Linux environment. Many of the Windows 200X/XP privileges have no direct equivalence in UNIX.

## 14.2 The Administrator Domain SID

Please note that every Windows NT4 and later server requires a domain Administrator account. Samba versions commencing with 3.0.11 permit Administrative duties to be performed via assigned rights and privileges (see Chapter 14, “User Rights and Privileges”). An account in the server's passdb backend can be set to the well-known RID of the default administrator account. To obtain the domain SID on a Samba domain controller, run the following command:

```
root# net getlocalsid
SID for domain F00 is: S-1-5-21-4294955119-3368514841-2087710299
```

You may assign the domain administrator RID to an account using the **pdbedit** command as shown here:

```
root# pdbedit -U S-1-5-21-4294955119-3368514841-2087710299-500 -u root -r
```

> NOTE
> The RID 500 is the well known standard value of the default Administrator account. It is the RID that confers the rights and privileges that the Administrator account has on a Windows machine or domain. Under UNIX/Linux the equivalent is UID=0 (the root account).
