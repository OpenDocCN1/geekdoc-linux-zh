gpgkey=https://www.mongodb.org/static/pgp/server-6.0.asc

+   2. Install the **MongoDB** packages:

```
`yum install -y mongodb-org`
```

*Figure 11.32* shows the partial output of the installation process:

```
`[root@rhel ~]# yum install -y mongodb-org  |  tail -15`  
Installed products updated.

Installed:
  compat-openssl11-1:1.1.1k-4.el9_0.x86_64
  cyrus-sasl-2.1.27-20.el9.x86_64
  mongodb-database-tools-100.6.0-1.x86_64
  mongodb-mongosh-1.6.0-1.el8.x86_64
  mongodb-org-6.0.1-1.el8.x86_64
  mongodb-org-database-6.0.1-1.el8.x86_64
  mongodb-org-database-tools-extra-6.0.1-1.el8.x86_64
  mongodb-org-mongos-6.0.1-1.el8.x86_64
  mongodb-org-server-6.0.1-1.el8.x86_64
  mongodb-org-tools-6.0.1-1.el8.x86_64

Complete!
```

*Figure 11.32: Output example installing MongoDB*

After the package for **MongoDB** is installed, it is needed to install the service **mongodb** using the command *systemctl*. *Figure 11.33* shows the output of the status of the service after starting it:

```
`root@ubuntu:~# systemctl start mongod`  
`root@ubuntu:~# systemctl status mongod`  
 `● mongod.service - MongoDB Database Server`  
`   Loaded: loaded (/lib/systemd/system/mongod.service; disabled; vendor preset:` `)`  
`   Active: active (running) since Wed 2022-09-21 20:26:25 UTC; 3s ago`  
`     Docs: https://docs.mongodb.org/manual`  
`  Main PID: 5531 (mongod)`  
`   Memory: 63.8M`  
`      CPU: 176ms`  
`   CGroup: /system.slice/mongod.service`  
`           └─5531 /usr/bin/mongod --config /etc/mongod.conf`  

Sep 21 20:26:25 ubuntu systemd[1]: Started MongoDB Database Server.
```

*Figure 11.33: Output example for systemctl command*