
Due to a limitation in Samba's **smb.conf** parsing, you should not surround the domain names with quotation marks.

## 34.4.4.3 IdMap LDAP Support

Samba-3 supports an LDAP backend for the idmap subsystem. The following options inform Samba that the idmap table should be stored on the directory server *onterose* in the *ou=idmap,dc=quenya,dc=org* partition.

```ini
[global]
...
  idmap backend = ldap:ldap://onterose/
  ldap idmap suffix = ou=idmap,dc=quenya,dc=org
  idmap uid = 40000-50000
  idmap gid = 40000-50000
```

This configuration allows Winbind installations on multiple servers to share a UID/GID number space, thus avoiding the interoperability problems with NFS that were present in Samba-2.2.

## MIGRATION FROM NT4 PDC TO SAMBA-3 PDC

This is a rough guide to assist those wishing to migrate from NT4 domain control to Samba-3-based domain control.

### 35.1 Planning and Getting Started

In the IT world there is often a saying that all problems are encountered because of poor planning. The corollary to this saying is that not all problems can be anticipated and planned for. Then again, good planning will anticipate most show-stopper-type situations.

Those wishing to migrate from MS Windows NT4 domain control to a Samba-3 domain control environment would do well to develop a detailed migration plan. So here are a few pointers to help migration get underway.

#### 35.1.1 Objectives

The key objective for most organizations is to make the migration from MS Windows NT4 to Samba-3 domain control as painless as possible. One of the challenges you may experience in your migration process may well be convincing management that the new environment should remain in place. Many who have introduced open source technologies have experienced pressure to return to a Microsoft-based platform solution at the first sign of trouble.

Before attempting a migration to a Samba-3-controlled network, make every possible effort to gain all-round commitment to the change. Know precisely why the change is important for the organization. Possible motivations to make a change include:

- Improve network manageability.
- Obtain better user-level functionality.
- Reduce network operating costs.
- Reduce exposure caused by Microsoft withdrawal of NT4 support.
- Avoid MS License 6 implications.
- Reduce organization’s dependency on Microsoft.

Make sure everyone knows that Samba-3 is not MS Windows NT4. Samba-3 offers an alternative solution that is both different from MS Windows NT4 and offers advantages compared with it. Gain recognition that Samba-3 lacks many of the features that Microsoft has promoted as core values in migration from MS Windows NT4 to MS Windows 2000 and beyond (with or without Active Directory services).

What are the features that Samba-3 cannot provide?

- Active Directory Server.
- Group Policy Objects (in Active Directory).
- Machine Policy Objects.
- Logon Scripts in Active Directory.
- Software Application and Access Controls in Active Directory.

The features that Samba-3 does provide and that may be of compelling interest to your site include:

- Lower cost of ownership.
- Global availability of support with no strings attached.
- Dynamic SMB servers (can run more than one SMB/CIFS server per UNIX/Linux system).
- Creation of on-the-fly logon scripts.
- Creation of on-the-fly policy files.
- Greater stability, reliability, performance, and availability.
- Manageability via an SSH connection.
- Flexible choices of backend authentication technologies (tdbsam, ldapsam, mysqlsam).
- Ability to implement a full single-sign-on architecture.
- Ability to distribute authentication systems for absolute minimum wide-area network bandwidth demand.

Before migrating a network from MS Windows NT4 to Samba-3, consider all necessary factors. Users should be educated about changes they may experience so the change will be a welcome one and not become an obstacle to the work they need to do. The following sections explain factors that will help ensure a successful migration.

##### 35.1.1.1 Domain Layout

Samba-3 can be configured as a domain controller, a backup domain controller (probably best called a secondary controller), a domain member, or a standalone server. The Windows network security domain context should be sized and scoped before implementation. Particular attention needs to be paid to the location of the Primary Domain Controller (PDC) as well as backup controllers (BDCs). One way in which Samba-3 differs from Microsoft technology is that if one chooses to use an LDAP authentication backend, then the same database can be used by several different domains. In a complex organization, there can be a single LDAP database, which itself can be distributed (have a master server and multiple slave servers) that can simultaneously serve multiple domains.

From a design perspective, the number of users per server as well as the number of servers per domain should be scaled taking into consideration server capacity and network bandwidth.

A physical network segment may house several domains. Each may span multiple network segments. Where domains span routed network segments, consider and test the performance implications of the design and layout of a network. A centrally located domain controller that is designed to serve multiple routed network segments may result in severe performance problems. Check the response time (ping timing) between the remote segment and the PDC. If it's long (more than 100 ms), locate a BDC on the remote segment to serve as the local authentication and access control server.

##### 35.1.1.2 Server Share and Directory Layout

There are cardinal rules to effective network design that cannot be broken with impunity. The most important rule: Simplicity is king in every well-controlled network. Every part of the infrastructure must be managed; the more complex it is, the greater will be the demand of keeping systems secure and functional.

Keep in mind the nature of how data must be shared. Physical disk space layout should be considered carefully. Some data must be backed up. The simpler the disk layout, the easier it will be to keep track of backup needs. Identify what backup media will meet your needs; consider backup to tape, CD-ROM or DVD-ROM, or other offline storage medium. Plan and implement for minimum maintenance. Leave nothing to chance in your design; above all, do not leave backups to chance: backup, test, and validate every backup; create a disaster recovery plan and prove that it works.

Users should be grouped according to data access control needs. File and directory access is best controlled via group permissions, and the use of the "sticky bit" on group-controlled directories may substantially avoid file access complaints from Samba share users.

Inexperienced network administrators often attempt elaborate techniques to set access controls on files, directories, shares, as well as in share definitions. Keep your design and implementation simple and document your design extensively. Have others audit your documentation. Do not create a complex mess that your successor will not understand. Remember, job security through complex design and implementation may cause loss of operations and downtime to users as the new administrator learns to untangle your knots. Keep access controls simple and effective, and make sure that users will never be interrupted by obtuse complexity.

##### 35.1.1.3 Logon Scripts

Logon scripts can help to ensure that all users gain the share and printer connections they need.

Logon scripts can be created on the fly so all commands executed are specific to the rights and privileges granted to the user. The preferred controls should be effected through group membership so group information can be used to create a custom logon script using the `root` `preexec` parameters to the `NETLOGON` share.

Some sites prefer to use a tool such as **kixstart** to establish a controlled user environment. In any case, you may wish to do a Google search for logon script process controls. In particular, you may wish to explore the use of the Microsoft Knowledge Base article KB189105 that deals with how to add printers without user intervention via the logon script process.

##### 35.1.1.4 Profile Migration/Creation

User and group profiles may be migrated using the tools described in the section titled Desktop Profile Management.

Profiles may also be managed using the Samba-3 tool **profiles**. This tool allows the MS Windows NT-style security identifiers (SIDs) that are stored inside the profile `NTuser.DAT` file to be changed to the SID of the Samba-3 domain.

##### 35.1.1.5 User and Group Accounts

It is possible to migrate all account settings from an MS Windows NT4 domain to Samba-3. Before attempting to migrate user and group accounts, you are STRONGLY advised to create in Samba-3 the groups that are present on the MS Windows NT4 domain **AND** to map them to suitable UNIX/Linux groups. By following this simple advice, all user and group attributes should migrate painlessly.

#### 35.1.2 Steps in Migration Process

The approximate migration process is described below.

- You have an NT4 PDC that has the users, groups, polices, and profiles to be migrated.
- Samba-3 is set up as a domain controller with netlogon share, profile share, and so on. Configure the `smb.conf` file to function as a BDC: `domain master = No`.

THE ACCOUNT MIGRATION PROCESS

1. Create a BDC account in the old NT4 domain for the Samba server using NT Server Manager. *Samba must not be running.*
2. `net rpc join -S NT4PDC -w DOMAIN -U Administrator%passw`
3. `net rpc vampire -S NT4PDC -U administrator%password`
4. `pdbedit -L` Note: Did the users migrate?
