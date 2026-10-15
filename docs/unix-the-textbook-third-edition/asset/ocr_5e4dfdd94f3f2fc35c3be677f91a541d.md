FMRI: pkg://solaris/web/server/apache-22@2.2.27,5.11-0.175.2.0.0.42.1:20140623T022811Z

# 9. Check the IP address of the new zone.

```
root@appzone:~# ipadm show-addr
ADDROBJ   TYPE    STATE       ADDR
lo0/v4    static  ok          127.0.0.1/8
net0/v4   dhcp    ok          192.168.0.26/24
lo0/v6    static  ok          ::1/128
net0/v6   addrconf ok
fe80::8:20ff:fed3:3836/10
```

# 10. Leave the new zone and return to the global zone.

```
root@appzone:~# exit
logout
[Connection to zone 'appzone' pts/2 closed]
root@solaris:~#
```

Conclusions: We created a new Solaris zone and downloaded and installed the Apache web server application into it.

# EXERCISE 25.6

Install the package gnu-emacs into the zone named appzone created in Example 25.5.

# 25.4 VIRTUALBOX

VirtualBox is a software virtualization tool that can be used to install other OSs as guests on a host computer system, running either of our two base UNIX systems. We first discuss what advantages the VirtualBox method of virtualization provides, and then define some basic terms used in it. Finally, using an example-based format, we detail the installation and basic usage of VirtualBox on PC-BSD and Solaris.

Why use VirtualBox virtualization?

The advantages of the kind of virtual environment that VirtualBox gives you are:

+   - You can run multiple OSs simultaneously. VirtualBox allows you to run more than one OS at a time. You can switch between OS environments by simply moving your mouse into the window that contains one of the operating systems!

+   - From the system security point of view, you can isolate a particular application, such as a Web server or FTP site inside a VirtualBox guest, and anything that intrudes on its operation from the Internet only infects the guest system. VirtualBox is similar to using the PC-BSD iocage and jails, and Solaris zones.

+   - Once installed, a VM and its virtual hard disks can be considered a "sandbox" that can be arbitrarily frozen, unfrozen, copied, backed up, and moved between hosts. With "snapshots," you can save a particular state of a VM and revert back to that state, if necessary.