# klist 569

# klist - List Currently Held Kerberos Tickets

# Synopsis

```
/usr/bin/klist [-e] [-c] [cache_name] [-f] [-s]
-k [-t] [keytab_file] [-K]
```

# Description

Use klist command to print the name of the credentials cache and the identity of the principal that the tickets are (as listed in the ticket file). The command also lists the principal names of all Kerberos tickets currently held by the user along with the issue and expiration time for each authenticator. Principal names are listed in the form name/Instance@realm, with the slash (/) omitted if the instance is not included and at the sign (@) omitted if the realm is not included.

If you do not specify cache_file or keytab_name, klist displays the credentials in the default credentials cache or keytab files, where uid is the current user ID. The above changes are new in the Solaris 8 release.

# Bugs

When a file is read as a key file, little error checking is performed.

# Options

+   -c [cache_name]
List tickets held in a credentials cache. This option is the default if you specify neither -c nor -k.

+   -e
Display the encryption types of the session key and the ticket for each credential in the credential cache, or each key in the keytab file.

+   -f
Show the flags in the credentials, using the following abbreviations:
F Forwardable.
f Forwarded.
P Proxyable.
P Proxy.
D Postdateable.
d Postdated.
R Renewable.
I Initial.
i Invalid.

+   -k [keytab_file]
List keys held in a keytab file.

+   -K
Display the value of the encryption key in each keytab entry in the keytab file.