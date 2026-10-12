well as which hosts are allowed to connect into the authsrv program running on the database.

```
authsrv:      permit hosts 127.0.0.1
authsrv:      permit hosts 128.83.155.45
authsrv:      database /var/adm/authsrv.db

# clients using the auth server
*: authserver 127.0.0.1 7777
```

By default, only the localhost is able to connect to the authsrv process. For this configuration, the localhost as well as the host 128.83.155.45 are allowed to connect to the authsrv server process. Furthermore, the database is located in /var/adm/authsrv.db. To initialize the database, run the authsrv program as root:

```
# ./authsrv
# authsrv# adduser admin "AuthSrv_Admin"
ok - user added initially disabled
authsrv# ena admin
enabled
authsrv# proto admin pass
changed
authsrv# pass admin "r8uT3&4M"
password changed
authsrv# superwiz admin
set wizard
authsrv# adduser ruser "Remote_User"
ok - user added initially disabled
authsrv# group ruser rgroup
ok - user added to group rgroup
authsrv# ena ruser
enabled
authsrv# proto ruser pass
changed
authsrv# pass ruser "L83A47!"
authsrv# list
user  group  longname      ok?  proto  last
.... .... .... .... .... ....
admin rgroup AuthSrv_Admin ena  passw never
ruser rgroup Remote_User   ena  passw never
authsrv# quit
#
```