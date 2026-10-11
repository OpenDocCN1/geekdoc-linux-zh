default_real variable in the `/etc/krb5.conf` file. To obtain a ticket for a different principal, specify the principal name on the command line, as in the following example:

```
[ramon]$ kinit alice@SYBEX.COM
```

The `klist` commands shows that the ticket you’ve just acquired is valid until 2/25/01 at 3:39 A.M. (10 hours from now). If you want to discard this ticket, use the `kdestroy` command to delete it from the cache (see Listing 13.10).

# **Listing 13.10** Deleting a ticket from the cache using `kdestroy`

```
```
[ramon]$ kdestroy
[ramon]$ klist
klist: No credentials cache file found (ticket cache FILE:/tmp/krb5cc_500)

Kerberos 4 ticket cache: /tmp/tkt500
klist: You have no tickets cached
```
```

Finally, the `kpasswd` command should be used by non-privileged members on a regular basis to change their Kerberos password to minimize its exposure. The use of the `kpasswd` utility is virtually identical to the use of the standard Linux `passwd` command, as you can see in Listing 13.11.

# **Listing 13.11** Changing a Kerberos password with `kpasswd`

```
```
[ramon]$ kpasswd
kpasswd: No credentials cache file found getting principal from: cache
[ramon]$ kinit
Password for ramon@HONTANON.COM:
[ramon]$ kpasswd
Password for ramon@HONTANON.COM:
Enter new password:
Enter it again:
Password changed.
```
```

Note that in order to issue the `kpasswd` command, you need to be in possession of an unexpired TGT. This makes sense because you’ll need this TGT to prove to the KDC that it really is you issuing the `kpasswd` command, and you’ll need the TGT to encrypt the new password while in transit.

> **WARNING** It is extremely important that you choose a good password and that you change it on a regular basis. Unlike your standard Linux password, the Kerberos password can be used to obtain tickets to access other services on your behalf, so the potential damage from an intrusion is much greater.