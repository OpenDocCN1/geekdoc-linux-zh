```
zone "yourdomain.com" {
    type master;
    file "mydomain.dns";
    allow-query  { any; };
    allow-update  { none; };
    allow-transfer { dns-ip-list; };
};
```

Unfortunately, malicious hackers can use IP spoofing tricks to trick a DNS server into performing a zone transfer. This potential calamity can now be avoided by using transaction signatures. Say that you want to limit the zone transfer for a domain called yourdomain.com to two secondary name servers with IP address 172.20.15.100 (ns1.yourdomain.com) and 172.20.15.123 (ns2.yourdomain.com).

![](bbox=[0.07, 0.62, 0.18, 0.72])

> You must make sure that the DNS servers involved in TSIG-based zone transfer authentication are kept time synchronized. You can create a cron job entry to synchronize each machine with a remote time server using rdate or ntp tools

The following steps show you how to use TSIG to ensure that IP spoofing tricks can't force a zone transfer between your DNS server and a hacker's DNS server.

+   1. Generate a shared secret key, which will be used to authenticate the zone transfer. Change directory to /var/named. Use the /usr/local/sbin/dnssec-keygen command to generate a set of public and private keys as follows:
+   
+   dnssec-keygen -a hmac-md5 -b 128 -n HOST zone-xfr-key
+   
+   The public key file is called Kzone-xfr-key.+157+08825.key and the private key file is Kzone-xfr-key.+157+08825.private. If you view the contents of the private key file you will see something similar to the following:
+   
+   Private-key-format: v1.2
+   Algorithm: 157 (HMAC_MD5)
+   Key: YH80nz5x0/twQnvYPyh1qg==