# NOTE

When user rights and privileges are correctly set, there is no longer a need for a Windows network account for the root user (nor for any synonym of it) with a UNIX UID=0. Initial user rights and privileges can be assigned by any account that is a member of the Domain Admins group. Rights can be assigned to user as well as group accounts.

![](bbox=[0.08, 0.14, 0.14, 0.19])

By default, no privileges and rights are assigned. This is demonstrated by executing the command shown here:

```
root# net rpc rights list accounts -U root%\not24get
BUILTIN\Print Operators
No privileges assigned

BUILTIN\Account Operators
No privileges assigned

BUILTIN\Backup Operators
No privileges assigned

BUILTIN\Server Operators
No privileges assigned

BUILTIN\Administrators
No privileges assigned

Everyone
No privileges assigned
```

The net command can be used to obtain the currently supported capabilities for rights and privileges using this method:

```
root# net rpc rights list -U root%\not24get
SeMachineAccountPrivilege    Add machines to domain
SePrintOperatorPrivilege    Manage printers
SeAddUserPrivilege          Add users and groups to the domain
SeRemoteShutdownPrivilege   Force shutdown from a remote system
SeDiskOperatorPrivilege     Manage disk shares
SeBackupPrivilege           Back up files and directories
SeRestorePrivilege          Restore files and directories
SeTakeOwnershipPrivilege    Take ownership of files or other objects
```