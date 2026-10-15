

that new zone. The example details the use of the pkg install command to do the installation.

We do not show the detailed use of the Apache web server.

## Prerequisites:
- 1. You must have completed Example 25.4.
- 2. Your Solaris system must be connected to the Internet, and you must have access to an Oracle Solaris IPS online repository.

Procedures: Do the following steps, in the order presented here, to meet the objectives of this example.

- 1. Create a zone, named appzone, using a minimum amount of information.

```
root@solaris:~# zonecfg -z appzone "create ; set zoneroot=/zones/appzone"
```

- 2. Use the zonecfg command to get information about the new zone.

```
root@solaris:~# zonecfg -z appzone info
zonename: appzone
zoneroot: /zones/appzone
...
Output truncated...
```

- 3. Install the zone, as in Example 25.4, from an online Oracle IPS repository.

```
root@solaris:~# zoneadm -z appzone install
The following ZFS file system(s) have been created:
 rpool/zones/appzone
Progress being logged to /var/log/zones/
zoneadm.20141017T110817Z.appzone.install
 Image: Preparing at /zones/appzone/root.
 Install Log: /system/volatile/install.4635/install_log
 AI Manifest: /tmp/manifest.xml.YJ4abj
 SC Profile: /usr/share/auto_install/sc_profiles/enable_sci.xml
 Zonename: appzone
 Installation: Starting ...
 Creating IPS image
 Startup linked: 1/1 done
 Installing packages from:
 solaris
 origin: http://pkg.oracle.com/solaris/release/
 DOWNLOAD PKGS FILES XFER (MB) SPEED
 Completed 282/282 53274/53274 351.9/351.9 3.4M/s
```

```
PHASE                                      ITEMS
Installing new actions                         71043/71043
Updating package state database                Done
Updating package cache                         0/0
Updating image state                          Done
Creating fast lookup database                 Done
Updating package cache                         1/1
Installation: Succeeded

        Note: Man pages can be obtained by installing
pkg:/system/manual
        done.

        Done: Installation completed in 346.285 seconds.
Next Steps: Boot the zone, then log into the zone
console (zlogin -C)
        to complete the configuration process.
Log saved in non-global zone as /zones/appzone/root/var/
log/zones/zoneadm.20141017T110817.appzone.install
```

4. Boot, or start, the new zone, log into it, and configure it with the same settings as Example 25.3. But, this time, use a different IP address: 192.168.0.26. Recall from Example 25.3 that the first three fields of the IP address of the new zone should be the same as the first three fields of the host IP address. This will put the zone on the same subnetwork as the host, which is mandatory if you want to access the application in the zone through the host NIC. Remember to leave the login console by typing ~. on the command line.

```
root@solaris:~# zoneadm -z appzone boot; zlogin -C appzone
[Connected to zone 'appzone' console]
Loading smf(5) service descriptions: 134/134
System Configuration window opens...
Make your choices...
SC profile successfully generated as:
/etc/svc/profile/sysconfig/sysconfig-20141017-112005/
sc_profile.xml
Exiting System Configuration Tool. Log is available at:
/system/volatile/sysconfig/sysconfig.log.6274
<Output truncated...>
Oct 17 04:25:09 appzone sendmail[8419]: unable to qualify
my own domain name (appzone) -- using short name
appzone console login: ~.
[Connection to zone 'appzone' console closed]
```

5. Log into the zone with zlogin.

```
root@solaris:~# zlogin appzone
[Connected to zone 'appzone' pts/2]
Oracle Corporation        SunOS 5.11   11.2   June 2014
```

FMRI: pkg://solaris/web/server/apache-22@2.2.27,5.11-0.175.2.0.0.42.1:20140623T022811Z

## 9. Check the IP address of the new zone.

```
root@appzone:~# ipadm show-addr
ADDROBJ   TYPE    STATE       ADDR
lo0/v4    static  ok          127.0.0.1/8
net0/v4   dhcp    ok          192.168.0.26/24
lo0/v6    static  ok          ::1/128
net0/v6   addrconf ok
fe80::8:20ff:fed3:3836/10
```

## 10. Leave the new zone and return to the global zone.

```
root@appzone:~# exit
logout
[Connection to zone 'appzone' pts/2 closed]
root@solaris:~#
```

Conclusions: We created a new Solaris zone and downloaded and installed the Apache web server application into it.

## EXERCISE 25.6

Install the package gnu-emacs into the zone named appzone created in Example 25.5.

## 25.4 VIRTUALBOX

VirtualBox is a software virtualization tool that can be used to install other OSs as guests on a host computer system, running either of our two base UNIX systems. We first discuss what advantages the VirtualBox method of virtualization provides, and then define some basic terms used in it. Finally, using an example-based format, we detail the installation and basic usage of VirtualBox on PC-BSD and Solaris.

Why use VirtualBox virtualization?

The advantages of the kind of virtual environment that VirtualBox gives you are:

- You can run multiple OSs simultaneously. VirtualBox allows you to run more than one OS at a time. You can switch between OS environments by simply moving your mouse into the window that contains one of the operating systems!

- From the system security point of view, you can isolate a particular application, such as a Web server or FTP site inside a VirtualBox guest, and anything that intrudes on its operation from the Internet only infects the guest system. VirtualBox is similar to using the PC-BSD iocage and jails, and Solaris zones.

- Once installed, a VM and its virtual hard disks can be considered a "sandbox" that can be arbitrarily frozen, unfrozen, copied, backed up, and moved between hosts. With "snapshots," you can save a particular state of a VM and revert back to that state, if necessary.

