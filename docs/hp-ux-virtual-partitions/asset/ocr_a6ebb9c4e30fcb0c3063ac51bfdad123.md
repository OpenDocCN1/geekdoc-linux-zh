```
zone "1.1.10.IN-ADDR.ARPA" {
    type slave;
    file "db.10.1.1";
    masters ( 15.17.186.159 );
};

zone "2.1.10.IN-ADDR.ARPA" {
    type slave;
    file "db.10.1.2";
    masters ( 15.17.186.159 );
};

zone "3.1.10.IN-ADDR.ARPA" {
    type slave;
    file "db.10.1.3";
    masters ( 15.17.186.159 );
};

zone "186.17.15.IN-ADDR.ARPA" {
    type slave;
    file "db.15.17.186";
    masters ( 15.17.186.159 );
};

zone "" {
    type hint;
    file "db.cache";
};
```

2. Now, all you need to do, once your named.boot has been copied to /etc/named.boot and your /etc/named.data directory has been created, is kick off a zone transfer. To kick off a zone transfer, all you need to do is kill named with

```
# sig_named restart
```

or

```
# kill -HUP ` /var/run/named.pid `
```

to start the transfer. Take a look at /etc/named.data and you should see all the database files there now. Also, check /var/adm/syslog/syslog.log to make sure the zones were loaded properly as shown in the following example: