![](bbox=[0.15, 0.1, 0.86, 0.5])

Figure 21. Social Media - MegaCorp One

Let’s update our notes to keep track of each of these bits of information including the email address format and social media sites references.

# 6.3 Whois Enumeration

Whois$^{139}$ is a TCP service, tool, and a type of database that can provide information about a domain name, such as the *name server*${}^{140}$ and *registrar*;$^{141}$ This information is often public since registrars charge a fee for private registration.

We can gather basic information about a domain name by executing a standard forward search by passing the domain name, *megacorpone.com*, into the **whois** client:

```
kali@kali:~$ whois megacorpone.com
Domain Name: MEGACORPONE.COM
Registry Domain ID: 1775445745_DOMAIN.COM-VRSN
Registrar WHOIS Server: whois.gandi.net
Registrar URL: http://www.gandi.net
Updated Date: 2019-01-01T09:45:03Z
```

+   139 (Wikipedia, 2019) https://en.wikipedia.org/wiki/WHOIS
+   140 (Wikipedia, 2019) https://en.wikipedia.org/wiki/Name_server
+   141 (Wikipedia, 2019) https://en.wikipedia.org/wiki/Domain_name_registrar