# 36 Part I: Hacking Techniques and Defenses

After performing port scans on target hosts, an intruder will know exactly which hosts are alive and what ports they have. Armed with this information, the logical next step is to enumerate information such as usernames, file shares, and operating system version numbers from services listening on the specific ports. Only after obtaining such information may an attacker move on exploiting particular vulnerabilities as discussed in the next chapter.

Many remote daemons display a banner message when a connection is made to the port they are listening on. Banner messages can give up information about services, such as their identity and version information. The process of obtaining banners from remote services is known as banner grabbing. Since most daemons allow their banners to be changed, you should take advantage of this capability.

Although it is a good idea to change server banners in order to confuse potential intruders, keep in mind that it will not deter the more sophisticated attackers.

# ENUMERATE REMOTE SERVICES

What follows is a list of services that are known to be susceptible to enumeration. They are sorted by the port numbers they usually listen on (see the file /etc/services on your Unix or Linux host for a comprehensive list).

> Any of the services listed here can be configured to listen on a nonstandard port. Some services use non-ASCII characters to communicate, and are difficult to identify. Tools such as Amap, available at http://www.thehackerschoice.com/releases.php, can be used to detect services:

```
$bash] amap -sT intranet.somecompanyasanexample.com 9934
Total amount of tasks to perform: 15
Amap1.2.1b started at Sun Mar 9 09:30:22 2003, stand back and keepnthe children away.
Protocol on IP 192.168.1.3 port 9934 tcp matches ssl
Protocol on IP 192.168.1.3 port 9934 tcp matches http
Unidentified ports: None.
Amap1.2.1b ended at Sun Mar 9 09:30:59 2003
```

In this example, Amap successfully discovered that host intranet .somecompanyasanexample.com was running HTTPS on port 9934. This is useful information, since the standard port for HTTPS is 443.