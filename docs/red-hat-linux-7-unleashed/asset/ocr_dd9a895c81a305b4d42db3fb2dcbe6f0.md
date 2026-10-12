Access the `/mnt/cdrom/RedHat/RPMS` directory:

```
`[root@server /root]# cd /mnt/cdrom/RedHat/RPMS`
```

Install the `RPMS yp-tools-2.4-4.1386.rpm, ypbind-1.6-11.1386.rpm`, and `ypserv-1.3.11-9.1386.rpm` with the following commands:

```
`[root@server RPMS]# rpm -i yp-tools-2-4-4.1386.rpm
[root@server RPMS]# rpm -i ypbind-1.6-11.1386.rpm
[root@server RPMS]# rpm -i ypserv-1.3.11-9.1386.rpm`
```

After the software is installed, the next step is configuring the master NIS server.

# Configuring a Master NIS Server

Before you configure the server software, you need to decide whether you are going to set up any slave servers. If you are, you need to know their hostnames before continuing. Along with the names of your NIS servers, you need to decide on a NIS domain name at this point. Remember that this domain name is not the same as your DNS domain name and for clarity should be set differently. Also, the names must be in the `/etc/hosts` file.

With this information, you are ready to begin. First, you need to set the domain name with the `domainname` command:

```
`[root@vestax /etc]# domainname audionet.domain.com`
```

Although this will work for the moment, you do need to change a startup configuration file so that this happens every time your system reboots. The `/etc/init.d/ypserv` script that was installed as part of the RPM looks for the domain name to be set in the `/etc/sysconfig/network` file. Simply add the following line:

```
`NISDOMAIN="audionet.domain.com"`
```

With the domain name set, you can decide what files you want to share via NIS, as well as their filenames. You do this by editing `/var/yp/Makefile`. As the name implies, NIS maintains its maps by using the `make` utility. Although familiarity with how this tool works is useful, it isn't mandatory in order to configure NIS.

Begin by loading `/var/yp/Makefile` into your favorite editor. Scroll past the lines that read as follows:

```
`# These are files from which the NIS databases are built. You may edit
# these to taste in the event that you wish to keep your NIS source files
# separate from your NIS server's actual configuration files.`
```