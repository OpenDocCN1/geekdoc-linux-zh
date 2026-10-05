# # OffSec

Penetration Testing with Kali Linux

valuable time for the client. If you do so, it's vital to perform the scans in a structured way to not miss results or miss findings.

As before, we will begin with an nmap scan of the target machine.

```
kalikal:~# sudo nmap -sC -sV websrv1/nmap 192.168.50.244
Starting Nmap 7.92 (nmap.org) @ 2022-09-29 11:18 EDT
nmap scan report for 192.168.50.244
Host is up (0.11 latency).
Not shown: 998 closed tcp ports (reset)
PORT STATE VERSION
22/tcp open OpenSSH 8.9p1 Ubuntu (Ubuntu Linux; protocol 2.0)
ssh-hostkey:
256:ed2:6d:ff:a4:97:58:92:85:32:82:64:53:b2:d7:be:44 (ECDSA)
256:8d:6d:ff:a4:97:58:92:85:32:82:64:53:b2:d7:be:44 (ECDSA)
80/tcp open Apache 2.4.52 ((Ubuntu))
http-title: BEYOND Finances #8211; We provide financial freedom
_Requested resource was http://192.168.50.244/
http-server-header: Apache/2.4.52 (Ubuntu)
http-generator: WordPress 6.0.2
Service Info: OS: Linux; CPE: /:linux:kernel
```

Service detection performed. Please report any incorrect results at https://nmap.org/submit/
nmap done: 1 IP address (1 host) scanned in 19.51 seconds

The Nmap scan revealed only two ports: 22 and 80. Nmap fingerprinted the services as running an SSH service and HTTP service on the ports, respectively.

From the SSH banner, we retrieve the information that the target is running on an Ubuntu Linux system. However, the banner provides much more detail with a bit of manual work. Let copy the "OpenSSH 8.9p1 Ubuntu" to a search engine. The results contain a link to the Ubuntu Launchpad page which contains a list of OpenSSH version mapped to specific Ubuntu releases. In our example, the version is mapped to Jellyfish, which is the version name for Ubuntu 22.04.

![](bbox=[0.125, 0.663, 0.875, 0.723])

For port 22, we currently only have the option to perform a password attack. Because we don't have any username or password information, we should analyze other services first. Therefore, let's enumerate port 80 running Apache 2.4.52.

1178 (Launchpad, 2022), https://launchpad.com/ubuntu/+source/openssh

PWK - Copyright ©2023 OffSec Services Limited. All rights reserved.

811