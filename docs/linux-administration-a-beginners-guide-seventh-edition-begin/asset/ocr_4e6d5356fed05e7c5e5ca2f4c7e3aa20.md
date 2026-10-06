# 444 Linux Administration: A Beginner's Guide

+   - Define smtp.example.org as the mail exchanger (MX) for the example.org domain.
- Define www.example.org as an alternative name (CNAME) for serverA.example.org, and ftp.example.org as an alternative name for serverB.example.org.
- Define contact information for serverA.example.org.

Okay, Mr. Bond, you have your instructions. Go forth and complete the mission.
Good luck!

# DNS Server Setup Walk-Through

To accomplish our goal of setting up a DNS server for example.org, we will need to take a series of steps. Let's walk through them one at a time.

> TIP If you don't feel like much typing, we've bundled all the files that you need to follow and saved for you at the following URL. You just need to download, uncompress, and copy the files to the proper directories in the steps like:
```bash
# pwd
# wget http://linuxserverexperts.com/7e/chapter-16.tar.xz
# tar xvf chapter-16.tar.xz
# cd chapter-16 && ls
```

+   1. Make sure you have installed the BIND server software as described earlier in the chapter. Use the rpm command to confirm this:
```bash
[root@serverA ~]# rpm -q bind bind-9.*
```

> NOTE If you only built and installed BIND from source, the preceding rpm command will not reveal anything, because the RPM database will know nothing about it. But you would know what you installed and where.

+   2. Use any text editor you are comfortable with to create the main DNS configuration file—the /etc/named.conf file. Enter the following text into the file:
```
options {
    listen-on port 53 { any };
    listen-on-v6 port 53 { any };
    directory "/var/named";
    dump-file "/var/named/data/cache_dump.db";
    statistics-file "/var/named/data/named_stats.txt";
    notify yes;
}
```