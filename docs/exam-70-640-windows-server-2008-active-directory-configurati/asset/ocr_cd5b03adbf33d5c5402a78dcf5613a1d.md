# **Table 5-1 (continued)**

| GROUP NAME | GROUP SCOPE | LOCATION IN ACTIVE DIRECTORY | DEFAULT MEMBERS | PURPOSE | SPECIAL NOTES |
|---|---|---|---|---|---|
| Administrators | Domain local | Built-in container | Administrator account, Domain Admins global group from the specific domain, and the Enterprise Admins universal group | Members have complete and unrestricted access to the computer or domain controller locally, including the right to change their own permissions. | None |
| Backup Operators | Domain local | Built-in container | None | Members can back up and restore all files on a computer, regardless of the permissions that protect those files. Members can log on to the computer and shut it down. | None |
| Certificate Service DCOM Access | Domain local | Built-in container | None | Members are allowed to connect to Certification Authorities across the Active Directory forest. | None |
| Cryptographic Operators | Domain local | Built-in container | None | Members are allowed to perform cryptographic operations. | None |
| Distributed COM Users | Domain local | Built-in container | None | Members are permitted to use Distributed COM objects on all domain controllers. | None |
| Event Log Readers | Domain local | Built-in container | None | Members are permitted to read event logs from all domain controllers. | None |
| Guests | Domain local | Built-in container | Domain Guests global group and the Guests user account | Members have the same privileges as members of the Users group. | The Guest account is disabled by default. |
| IIS_IUSR$ | Domain local | Built-in container | IUSR special identity | Built-in group used by IIS. | None |
| Incoming Forest Trust Builders | Domain local | Built-in container | None | Members can create incoming, one-way trusts to this forest. | None |
| Network Configuration Operators | Domain local | Built-in container | None | Members have the same default rights as members of the Users group. Members can perform all tasks related to the client side of network configuration, except for installing and removing drivers and services. | Members cannot configure network server services, such as the Domain Name System (DNS) and DHCP server services. |

*(continued)*