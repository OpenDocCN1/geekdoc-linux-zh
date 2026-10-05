# OffSec Penetration Testing with Kali Linux

CONFERENCE01, we'll start a verbose (-ddd) Socat process. It will listen on TCP port 2345 (TCP-LISTEN:2345), forking a new subprocess when it receives a connection (fork) instead of dying after a single connection, forward all traffic it receives to port 5432 on PGDATABASE01(10.4.50.215:5432).

We'll listen on port 2345 as it's not in the privileged port range (0-1024), which means we don't need elevated privileges to use it.

```
confluence@confluence01:/opt/atlassian/confluence/bin$ socat -ddd TCP-LISTEN:2345,fork
10.4.50.215:5432
socat -ddd TCP-LISTEN:2345,fork 10.4.50.215:5432
2022/08/18 10:12:01 socat [46589] I process started by Gerhard Hierier and contributors - see
www.dest-reach.org
2022/08/18 10:12:01 socat [46589] This product includes software developed by the OpenSSL Project for use in the OpenSSL Toolkit (http://www.opens.org/)
2022/08/18 10:12:01 socat [46589] This product includes software written by Tim Hudson (tjh@cryptososoft.com)
2022/08/18 10:12:01 socat [46589] I setting option "fork" to 1
2022/08/18 10:12:01 socat [46589] I socket(2, 1, 6) -> 5
2022/08/18 10:12:01 socat [46589] I starting accept loop
2022/08/18 10:12:01 socat [46589] N listening:Running on AF=2 0.0.0.0:2345
```

The network is now set up like the following forward diagram:

![](bbox=[0.119, 0.513, 0.88, 0.715])

Figure 24: Socat in place as our port forwarder

With the Socat process running, we can run psql on our Kali machine, specifying that we want to connect to CONFERENCE01 (-h 192.168.50.63) on port (-p 2345) with the postgres account (-U postgres). When we are prompted for the password, and once connected, we can run the \ command to list the databases.

```
kali@kali:~$ psql -h 192.168.50.63 -p 2345 postgres
Password for user postgres:
psql (14.2) (Debian 12.1+b3), server 12.11 (Ubuntu 12.11-ubuntu0.20.04.1)
```