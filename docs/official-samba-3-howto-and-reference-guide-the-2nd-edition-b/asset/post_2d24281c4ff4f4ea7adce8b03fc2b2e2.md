
**Winbind is not used; users and groups resolved via NSS:** In this situation user and group accounts are treated as if they are local accounts. The only way in which this differs from having local accounts is that the accounts are stored in a repository that can be shared. In practice this means that they will reside in either an NIS-type database or else in LDAP.

This configuration may be used with standalone Samba servers, domain member servers (NT4 or ADS), and for a PDC that uses either an smpasswd or a tdbsam-based Samba passdb backend.

**Winbind/NSS with the default local IDMAP table:** There are many sites that require only a simple Samba server or a single Samba server that is a member of a Windows NT4 domain or an ADS domain. A typical example is an appliance like file server on which no local accounts are configured and winbind is used to obtain account credentials from the domain controllers for the domain. The domain control can be provided by Samba-3, MS Windows NT4, or MS Windows Active Directory.

Winbind is a great convenience in this situation. All that is needed is a range of UID numbers and GID numbers that can be defined in the *smb.conf* file. The *etc/nsswitch.conf* file is configured to use *winbind*, which does all the difficult work of mapping incoming SIDs to appropriate UIDs and GIDs. The SIDs are allocated a UID/GID in the order in which winbind receives them.

This configuration is not convenient or practical in sites that have more than one Samba server and that require the same UID or GID for the same user or group across all servers. One of the hazards of this method is that in the event that the winbind IDMAP file becomes corrupted or lost, the repaired or rebuilt IDMAP file may allocate UIDs and GIDs to different users and groups from what were there previously with the result that MS Windows files that are stored on the Samba server may no longer belong to the rightful owners.

**Winbind/NSS uses RID based IDMAP:** The IDMAP RID facility is new to Samba version 3.0.8. It was added to make life easier for a number of sites that are committed to use of MS ADS, that do not apply an ADS schema extension, and that do not have an installed an LDAP directory server just for the purpose of maintaining an IDMAP table. If you have a single ADS domain (not a forest of domains, and not multiple domain trees) and you want a simple cookie-cutter solution to the IDMAP table problem, then IDMAP RID is an obvious choice.

This facility requires the allocation of the *idmap uid* and the *idmap gid* ranges, and within the *idmap uid* it is possible to *allocate a subset* of this range for automatic mapping of the relative identifier (RID) portion of the SID directly to the base of the UID plus the RID value. For example, if the *idmap uid* range is *1000-10000000* and the *idmap backend* = *idmap_rid:DOMAIN_NAME*=*1000-50000000*, and a SID is encountered that has the value *S-1-5-21-34567898-12529001-32973135-1234*, the resulting UID will be *1000 + 1234* = *2234*.

**Winbind with an NSS/LDAP backend-based IDMAP facility:** In this configuration **winbind** resolved SIDs to UIDs and GIDs from the `idmap uid` and `idmap gid` ranges specified in the `smb.conf` file, but instead of using a local winbind IDMAP table, it is stored in an LDAP directory so that all domain member machines (clients and servers) can share a common IDMAP table.

It is important that all LDAP IDMAP clients use only the master LDAP server because the `idmap backend` facility in the `smb.conf` file does not correctly handle LDAP redirects.

**Winbind with NSS to resolve UNIX/Linux user and group IDs:** The use of LDAP as the passdb backend is a smart solution for PDC, BDC, and domain member servers. It is a neat method for assuring that UIDs, GIDs, and the matching SIDs are consistent across all servers.

The use of the LDAP-based passdb backend requires use of the PADL `nss_ldap` utility or an equivalent. In this situation `winbind` is used to handle foreign SIDs, that is, SIDs from standalone Windows clients (i.e., not a member of our domain) as well as SIDs from another domain. The foreign UID/GID is mapped from allocated ranges (`idmap uid` and `idmap gid`) in precisely the same manner as when using `winbind` with a local IDMAP table.

The `nss_ldap` tool set can be used to access UIDs and GIDs via LDAP as well as via Active Directory. In order to use Active Directory, it is necessary to modify the ADS schema by installing either the ADAUNIX schema extension or using the Microsoft Services for UNIX version 3.5 or later to extend the ADS schema so it maintains UNIX account credentials. Where the ADS schema is extended, a Microsoft Management Console (MMC) snap-in is also installed to permit the UNIX credentials to be set and managed from the ADS User and Computer Management tool. Each account must be separately UNIX-enabled before the UID and GID data can be used by Samba.

## 13.1.3 Primary Domain Controller

Microsoft Windows domain security systems generate the user and group SID as part of the process of creation of an account. Windows does not have a concept of the UNIX UID or a GID; rather, it has its own type of security descriptor. When Samba is used as a domain controller, it provides a method of producing a unique SID for each user and group. Samba generates a machine and a domain SID to which it adds an RID that is calculated algorithmically from a base value that can be specified in the `smb.conf` file, plus twice (2x) the UID or GID. This method is called "algorithmic mapping".

For example, if a user has a UID of 4321, and the algorithmic RID base has a value of 1000, the RID will be 1000 + (2 x 4321) = 9642. Thus, if the domain SID is S-1-5-21-89238497-92787123-12341112, the resulting SID is S-1-5-21-89238497-92787123-12341112-9642.

The foregoing type of SID is produced by Samba as an automatic function and is either produced on the fly (as is the case when using a `passdb backend = [tdbsam | smbpasswd]`), or may be stored as a permanent part of an account in an LDAP-based passdb.

ADS uses a directory schema that can be extended to accommodate additional account attributes such as UIDs and GIDs. The installation of Microsoft Service for UNIX 3.5 will expand the normal ADS schema to include UNIX account attributes. These must of course be managed separately through a snap-in module to the normal ADS account management MMC interface.

Security identifiers used within a domain must be managed to avoid conflict and to preserve integrity. In an NT4 domain context, the PDC manages the distribution of all security credentials to the backup domain controllers (BDCs). At this time the only passdb backend for a Samba domain controller that is suitable for such information is an LDAP backend.

## 13.1.4 Backup Domain Controller

BDCs have read-only access to security credentials that are stored in LDAP. Changes in user or group account information are passed by the BDC to the PDC. Only the PDC can write changes to the directory.

IDMAP information can be written directly to the LDAP server so long as all domain controllers have access to the master (writable) LDAP server. Samba-3 at this time does not handle LDAP redirects in the IDMAP backend. This means that it is unsafe to use a slave (replicate) LDAP server with the IDMAP facility.

## 13.2 Examples of IDMAP Backend Usage

Anyone who wishes to use `winbind` will find the following example configurations helpful. Remember that in the majority of cases `winbind` is of primary interest for use with domain member servers (DMSs) and domain member clients (DMCs).

### 13.2.1 Default Winbind TDB

Two common configurations are used:

- Networks that have an NT4 PDC (with or without BDCs) or a Samba PDC (with or without BDCs).
- Networks that use MS Windows 200x ADS.

#### 13.2.1.1 NT4-Style Domains (Includes Samba Domains)

Example 13.2.1 is a simple example of an NT4 DMS `smb.conf` file that shows only the global section.

The use of `winbind` requires configuration of NSS. Edit the `/etc/nsswitch.conf` so it includes the following entries:
