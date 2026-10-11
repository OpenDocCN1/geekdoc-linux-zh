Now we just need to add these locations to `slapd.conf`, anywhere before the **database** declaration as shown here:

```
TLSCertificateFile /etc/openldap/server.crt.pem
TLSCertificateKeyFile /etc/openldap/serverkey.pem
TLSCACertificateFile /etc/openldap/cacert.pem
```

Here is the declaration and `ldap.conf`: `ldap.conf`

```
TLS_CACERT /etc/openldap/cacert.pem
```

That’s all there is to it. Now on to Section 44.3

# ## 44.3 Testing

This is the easy part. Restart the server:

```
root# /etc/init.d/ldap restart
Stopping slapd:                                            [  OK  ]
Checking configuration files for slapd: config file testing succeeded
Starting slapd:                                           [  OK  ]
```

Then, using `ldapsearch`, test an anonymous search with the `--ZZ`⁷ option:

```
root#  ldapsearch -x -b "dc=ldap,dc=abmas,dc=biz" \
         -H 'ldap://ldap.abmas.biz:389' --ZZ
```

Your results should be the same as before you restarted the server, for example:

> ⁷ See man ldapsearch