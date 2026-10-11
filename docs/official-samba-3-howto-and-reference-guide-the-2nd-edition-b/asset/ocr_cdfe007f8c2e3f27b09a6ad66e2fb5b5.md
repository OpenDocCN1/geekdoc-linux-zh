ads\_connect: No results returned
Join to domain is not valid

The specific error message may differ from the above because it depends on the type of failure that may have occurred. Increase the `log level` to 10, repeat the test, and then examine the log files produced to identify the nature of the failure.

+   4.  Start the `nmbd`, `winbind`, and `smbd` daemons in the order shown.

# 13.3.2 IDMAP\_RID with Winbind

The `idmap\_rid` facility is a new tool that, unlike native winbind, creates a predictable mapping of MS Windows SIDs to UNIX UIDs and GIDs. The key benefit of this method of implementing the Samba IDMAP facility is that it eliminates the need to store the IDMAP data in a central place. The downside is that it can be used only within a single ADS domain and is not compatible with trusted domain implementations.

This alternate method of SID to UID/GID mapping can be achieved using the `idmap\_rid` plug-in. This plug-in uses the RID of the user SID to derive the UID and GID by adding the RID to a base value specified. This utility requires that the parameter `allow trusted domains = No` be specified, as it is not compatible with multiple domain environments. The `idmap uid` and `idmap gid` ranges must be specified.

The `idmap\_rid` facility can be used both for NT4/Samba-style domains and Active Directory. To use this with an NT4 domain, do not include the `realm` parameter; additionally, the method used to join the domain uses the `net rpc join` process.

An example `smb.conf` file for and ADS domain environment is shown in Example 13.2.3.

# Example 13.2.3 ADS Domain Member smb.conf using idmap\_rid

```
```\n# Global parameters
[global]
        workgroup = KPAK
        netbios name = BIGJOE
        realm = CORP.KPAK.COM
        server string = Office Server
        security = ADS
        allow trusted domains = No
        idmap backend = idmap\_rid:KPAK=500-100000000
        idmap uid = 500-100000000
        idmap gid = 500-100000000
        template shell = /bin/bash
        winbind use default domain = Yes
        winbind enum users = No
        winbind enum groups = No
        winbind nested groups = Yes
        printer admin = "Domain Admins"
```
```