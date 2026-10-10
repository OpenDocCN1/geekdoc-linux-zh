# 7.5.3.2 APT

The Advanced Package Tool is a management system for software packages. The command line tool for handling packages is **apt-get**, which comes with an excellent man page describing how to install and update packages and how to upgrade singular packages or your entire distribution. APT has its roots in the Debian GNU/Linux distribution, where it is the default manager for the Debian packages. APT has been ported to work with RPM packages as well. The main advantage of APT is that it is free and flexible to use. It will allow you to set up systems similar to the distribution specific (and in some cases commercial) ones listed in the next sections.

Generally, when first using **apt-get**, you will need to get an index of the available packages. This is done using the command

```
```
apt-get update
```
```

After that, you can use **apt-get** to upgrade your system:

```
```
apt-get upgrade
```
```

Do this often, it's an easy way to keep your system up-to-date and thus safe.

Apart from this general usage, **apt-get** is also very fast for installing individual packages. This is how it works:

```
```
[david@jupiter ~]$ su - -c "apt-get install xsnow"
Password:
Reading Package Lists... Done
Building Dependency Tree... Done
The following NEW packages will be installed:
  xsnow
0 packages upgraded, 1 newly installed, 0 removed and 3 not upgraded.
Need to get 33.6kB of archives.
After unpacking 104kB of additional disk space will be used.
Get 1 http://ftp.freshsparks.net redhat/9/i386/0s xsnow 1.42-10 [33.6kB]
Fetched 33.6kB in 0s (106kB/s)
Executing RPM (-Uvh)...
  Preparing...                        ###########################################
 [100%]
   1:xsnow                          ###########################################
 [100%]
```
```

Note the **-c** option to the su command, which indicates to the root shell to only execute this command, and then return to the user's environment. This way, you cannot forget to quit the root account.

If there are any dependencies on other packages, **apt-get** will download and install these supporting packages.

More information can be found in the APT HOWTO <http://www.debian.org/doc/user-manuals#apt-howto>.