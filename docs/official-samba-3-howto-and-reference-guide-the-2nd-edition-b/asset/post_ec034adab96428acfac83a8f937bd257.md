
## NOTE

When user rights and privileges are correctly set, there is no longer a need for a Windows network account for the root user (nor for any synonym of it) with a UNIX UID=0. Initial user rights and privileges can be assigned by any account that is a member of the Domain Admins group. Rights can be assigned to user as well as group accounts.

![](img/86d74c6cc862465e3a42e6dc3c90935a_259_0.png)

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

Machine account privilege is necessary to permit a Windows NT 4.0 or later network client to be added to the domain. The disk operator privilege is necessary to permit the user to manage share ACLs and file and directory ACLs for objects not owned by the user.

In this example, all rights are assigned to the Domain Admins group. This is a good idea since members of this group are generally expected to be all-powerful. This assignment makes that the reality:

```
root# net rpc rights grant "MIDEARTH\Domain Admins" \
SeMachineAccountPrivilege SePrintOperatorPrivilege \
SeAddUserPrivilege SeRemoteShutdownPrivilege \
SeDiskOperatorPrivilege -U root%not24get
Successfully granted rights.
```

Next, the domain user jht is given the privileges needed for day-to-day administration:

```
root# net rpc rights grant "MIDEARTH\jht" \
SeMachineAccountPrivilege SePrintOperatorPrivilege \
SeAddUserPrivilege SeDiskOperatorPrivilege \
-U root%not24get
Successfully granted rights.
```

The following step permits validation of the changes just made:

```
root# net rpc rights list accounts -U root%not24get
MIDEARTH\jht
SeMachineAccountPrivilege
SePrintOperatorPrivilege
SeAddUserPrivilege
SeDiskOperatorPrivilege

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

- MIDEARTH\Domain Admins
  - SeMachineAccountPrivilege
  - SePrintOperatorPrivilege
  - SeAddUserPrivilege
  - SeRemoteShutdownPrivilege
  - SeDiskOperatorPrivilege

## 12.6 Managing Trust Relationships

There are essentially two types of trust relationships: the first is between domain controllers and domain member machines (network clients), the second is between domains (called interdomain trusts). All Samba servers that participate in domain security require a domain membership trust account, as do like Windows NT/2000/XP workstations.

### 12.6.1 Machine Trust Accounts

The net command looks in the **smb.conf** file to obtain its own configuration settings. Thus, the following command 'knows' which domain to join from the **smb.conf** file.

A Samba server domain trust account can be validated as shown in this example:

```
root#  net rpc testjoin
Join to 'MIDEARTH' is OK
```

Where there is no domain membership account, or when the account credentials are not valid, the following results will be observed:

```
net rpc testjoin -S DOLPHIN
Join to domain 'WORLDOCEAN' is not valid
```

The equivalent command for joining a Samba server to a Windows ADS domain is shown here:

```
root#  net ads testjoin
Using short domain name -- TAKEAWAY
Joined 'LEMONADE' to realm 'TAKEAWAY.BIZ'
```

In the event that the ADS trust was not established, or is broken for one reason or another, the following error message may be obtained:

```
root#  net ads testjoin -UAdministrator%secret
Join to domain is not valid
```

The following demonstrates the process of creating a machine trust account in the target domain for the Samba server from which the command is executed:

```
root#  net rcp join -S 13000 -Uroot%not24get
Joined domain MIDEARTH.
```

The joining of a Samba server to a Samba domain results in the creation of a machine account. An example of this is shown here:

```
root#  pdbedit -Lw merlin$
merlin$:1009:9B4489D6B90461FDBA3E3C3AB96147E16:\
      176DC8554E99914BDF3407DEA2231D80:[S          ]:LCT-42891919:
```

The S in the square brackets means this is a server (PDC/BDC) account. The domain join can be cast to join purely as a workstation, in which case the S is replaced with a W (indicating a workstation account). The following command can be used to affect this:

```
root#  net rcp join member -S 13000 -Uroot%not24get
Joined domain MIDEARTH.
```

Note that the command-line parameter *member* makes this join specific. By default the type is deduced from the *smb.conf* file configuration. To specifically join as a PDC or BDC, the command-line parameter will be [PDC | BDC]. For example:

```
root#  net rcp join bdc -S 13000 -Uroot%not24get
Joined domain MIDEARTH.
```

It is best to let Samba figure out the domain join type from the settings in the *smb.conf* file.

The command to join a Samba server to a Windows ADS domain is shown here:

```
root#  net ads join -UAdministrator%not24get
Using short domain name -- GDANSK
Joined 'FRANDIMITZ' to realm 'GDANSK.ABMAS.BIZ'
```

There is no specific option to remove a machine account from an NT4 domain. When a domain member that is a Windows machine is withdrawn from the domain, the domain membership account is not automatically removed either. Inactive domain member accounts can be removed using any convenient tool. If necessary, the machine account can be removed using the following **net** command:

```
root#  net rpc user delete HERRING\$ -Uroot%not24get
Deleted user account.
```

The removal is made possible because machine accounts are just like user accounts with a trailing $ character. The account management operations treat user and machine accounts in like manner.

A Samba-3 server that is a Windows ADS domain member can execute the following command to detach from the domain:

```
root#  net ads leave
```

Detailed information regarding an ADS domain can be obtained by a Samba DMS machine by executing the following:

```
root#  net ads status
```

The volume of information is extensive. Please refer to the book “Samba-3 by Example”. Chapter 7 for more information regarding its use. This book may be obtained either in print or online from the Samba-3 by Example<sup>1</sup>.

### 12.6.2 Interdomain Trusts

Interdomain trust relationships form the primary mechanism by which users from one domain can be granted access rights and privileges in another domain.

To discover what trust relationships are in effect, execute this command:

```
root#  net rpc trustdom list -Uroot%not24get
Trusted domains list:

none

Trusting domains list:
```

There are no interdomain trusts at this time; the following steps will create them.

It is necessary to create a trust account in the local domain. A domain controller in a second domain can create a trusted connection with this account. That means that the foreign domain is being trusted to access resources in the local domain. This command creates the local trust account:

```
root# net rpc trustdom add DAMNATION f00db4r -Uroot%\not24get
```

The account can be revealed by using the **pdbedit** as shown here:

```
root# pdbedit -Lw DAMNATION\$
DAMNATION\$ 1016 9ACF121DF897689AAD3B435B51404EE 7F845808B91BB9F7FEF44B247D9DC9A6 [I ] LCT-428934B1:
```

A trust account will always have an I in the field within the square brackets.

If the trusting domain is not capable of being reached, the following command will fail:

```
root# net rpc trustdom list -Uroot%\not24get
Trusted domains list:

none

Trusting domains list:

DAMNATION S-1-5-21-1385457007-882775198-1210191635
```

The above command executed successfully; a failure is indicated when the following response is obtained:

```
net rpc trustdom list -Uroot%\not24get
Trusted domains list:

DAMNATION S-1-5-21-1385457007-882775198-1210191635

Trusting domains list:

DAMNATION domain controller is not responding
```

> <sup>1</sup><http://www.samba.org/samba/docs/Samba3-ByExample.pdf>
