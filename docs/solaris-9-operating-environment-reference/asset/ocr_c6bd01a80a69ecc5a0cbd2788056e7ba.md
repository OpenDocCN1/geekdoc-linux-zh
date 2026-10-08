# kinit

# 567

| Time Duration Format | Example |
|---|---|
| #s | 30s |
| #d#h#m#s | 14d7h5m30s |
| #h#m[#s] | 7h5m30s |
| days-hh:mm:ss | 14-07:05:30 |
| hours:mm[:ss] | 7:05:30 |

| Delimiter | Description |
|---|---|
| d | Number of days. |
| h | Number of hours. |
| m | Number of minutes. |
| s | Number of seconds. |

| Variable | Description |
|---|---|
| # | Number. |
| days | Number of days. |
| hours | Number of hours. |
| hh | Hour (24-hour clock). |
| mm | Minutes. |
| ss | Seconds. |

The following example uses the kinit command to get the Ticket-Granting Ticket (TGT) for the user gmarler in the Kerberos realm gmarler.com.

> The user is already logged in under the user name gmarler.

```
$ kinit
Password for gmarler@GMARLER.COM: <principal password>
$
klist
Ticket cache: /tmp/krb5cc_11067
Default principal: gmarler@GMARLER.COM
```

Valid starting Expires
Service principal
Feb 26 08:09:12 2002 Feb 26 16:09:12 2002
krbtgt@GMARLER.COM@GMARLER.COM
renew until Tue Mar 05 08:09:12 2002

```
$
```