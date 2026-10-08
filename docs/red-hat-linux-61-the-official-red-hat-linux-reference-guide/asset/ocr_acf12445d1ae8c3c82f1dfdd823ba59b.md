# Chapter 13. Lightweight Directory Access Protocol (LDAP)

| Existing name service | Is LDAP running? | Script To Use |
| NetInfo | yes | migrate_all_netinfo_online.sh |
| NetInfo | no | migrate_all_netinfo_offline.sh |
| NIS (YP) | yes | migrate_all_nis_online.sh |
| NIS (YP) | no | migrate_all_nis_offline.sh |

Table 13-1. LDAP Migration Scripts

Run the appropriate script based on your existing name service.

> Note
You must have Perl installed on your system to use some of these scripts.

The README and the migration-tools.txt files in the `/usr/share/openldap/migration/` directory provides more details on how to migrate the information.

# 13.8. Upgrading to OpenLDAP Version 2.0

In OpenLDAP Version 2.0, the on-disk storage format used by the `ldap` LDAP server has changed. If you are upgrading LDAP from Red Linux 7.0 or earlier, you will need to extract the directory command to import this change into an LDIF file using the following:

```
ldbmcat -n > <ldif_file>
```

In the above command, change `<ldif_file>` to the name of the output file. Next type the following command to import this file into OpenLDAP 2.0:

```
slappadd -l <ldif_file>
```

> Important
You be the root user to use `/usr/sbin/slappadd`. However, the directory server runs as the `ldap` user. Therefore the directory server will not be able to modify any files created by `slappadd`. To correct this issue, after you finished using `slappadd`, type the following command:

```
chown -R ldap /var/lib/ldap
```

# 13.9. Additional Concerning Resources

More information concerning LDAP is available. Please review these sources, especially the OpenLDAP website and the LDAP HOWTO, before configuring LDAP on your system.