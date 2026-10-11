```
root# ldapmodify -x -h localhost \
-D "cn=Manager,dc={your-domain},dc={your-top-level-domain}" \
-W -f /path-to/foobar
```

Create a single-sided trust under the NT4 Domain User Manager, then execute:

```
root#  net rpc trustdom establish domain_name
```

It works with Samba-3 and NT4 domains, and also with Samba-3 and Windows 200x ADS in mixed mode. Both domain controllers, Samba and NT must have the same WINS server; otherwise, the trust will never work.