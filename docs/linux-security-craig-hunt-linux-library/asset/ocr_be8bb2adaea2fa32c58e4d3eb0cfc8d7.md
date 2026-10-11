To grant the principal ramon/admin@HONTANON.COM permission to change all of the database fields on any principal, add the following line:
ramon/admin@HONTANON.COM *

# The kadmin.local Utility

Next, you need to add an administrator to the Kerberos database using the kadmin.local utility. This utility is a command-line interface to the Kerberos administration server and it must be executed on the same host as the Kerberos KDC. The administrator principal that you choose to add must be present in the kadm5.acl file.

Once you enter the kadmin.local utility, a kadmin.local: prompt appears, where you can specify one of the following commands:

+   - addprinc principal: This command adds a new principal to the database.
+   - delprinc principal: This command deletes an existing principal from the database.
+   - modprinc principal: This command allows you to modify an existing principal.
+   - renprinc new old: This command renames a principal from new to old.
+   - cpw principal: This command allows you to change a principal's password.
+   - getprinc principal: This command displays a principal's record.
+   - listprincs: This command lists all principals in the database.
+   - ktadd -k keytab principal [principal]: This command adds one or more principal(s) to a keytab.
+   - ktremove -k keytab principal [principal]: This command removes one or more principal(s) from a keytab.

To create an administrator ramon/admin@HONTANON.COM, enter the following command.
In this example, the addprinc command adds a new principal to the Kerberos database with administrator privileges.

```
[ramon]$ sudo /usr/kerberos/sbin/kadmin.local
Authenticating as principal root/admin@HONTANON.COM with password.
  kadmin.local:  addprinc ramon/admin@HONTANON.COM
  Enter password for principal "ramon/admin@HONTANON.COM":
  Re-enter password for principal "ramon/admin@HONTANON.COM":
  Principal "ramon/admin@HONTANON.COM" created.
```

Next, you need to create a kadmnd keytab. A keytab is just a secret key that will be used by the Kerberos administration daemon (kadmnd) to decrypt the administrators' Kerberos tickets before granting them access to the Kerberos database. Note that there are two principals for whom you will be creating keytabs: kadmin/admin and