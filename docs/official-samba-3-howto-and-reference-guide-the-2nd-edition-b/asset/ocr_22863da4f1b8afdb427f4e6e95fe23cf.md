# 5.2.5.2 NetBIOS Over TCP/IP Disabled

An MS Windows NT4/2000/XP Professional workstation in the realm quemya.org that has a need to affect user login authentication will locate the domain controller by re-querying DNS servers for the ldap-tcp-pdc.msdc.s.quemya.org record. More information regarding this subject may be found in Section 9.3.3.

# 5.3 Backup Domain Controller Configuration

The creation of a BDC requires some steps to prepare the Samba server before smbd is executed for the first time. These steps are as follows:

+   The domain SID has to be the same on the PDC and the BDC. In Samba versions pre-2.2.5, the domain SID was stored in the file private/MACHINE.SID. For all versions of Samba released since 2.2.5 the domain SID is stored in the file private/secrets.tdb. This file is unique to each server and cannot be copied from a PDC to a BDC; the BDC will generate a new SID at startup. It will overwrite the PDC domain SID with the newly created BDC SID. There is a procedure that will allow the BDC to acquire the domain SID. This is described here.

To retrieve the domain SID from the PDC or an existing BDC and store it in the secrets.tdb, execute:

```
root# net rpc getsid
```

+   Specification of the ldap admin dn is obligatory. This also requires the LDAP administration password to be set in the secrets.tdb using the smbpasswd -w mysecret.

+   The ldap suffix parameter and the ldap idmap suffix parameter must be specified in the smb.conf file.

+   The UNIX user database has to be synchronized from the PDC to the BDC. This means that both the /etc/password and /etc/group have to be replicated from the PDC to the BDC. This can be done manually whenever changes are made. Alternately, the PDC is set up as an NIS master server and the BDC as an NIS slave server. To set up the BDC as a mere NIS client would not be enough, as the BDC would not be able to access its user database in case of a PDC failure. NIS is by no means the only method to synchronize passwords. An LDAP solution would also work.

+   The Samba password database must be replicated from the PDC to the BDC. Although it is possible to synchronize the smbpasswd file with rsync and ssh, this method is broken and flawed, and is therefore not recommended. A better solution is to set up slave LDAP servers for each BDC and a master LDAP server for the PDC. The use of rsync is inherently flawed by the fact that the data will be replicated at timed intervals. There is no guarantee that the BDC will be operating at all times with correct and current machine and user account information. This means that this method runs the risk of users being inconvenienced by discontinuity of access to network services due to