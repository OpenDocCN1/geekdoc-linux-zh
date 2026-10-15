```
zonecfg:firstzone> set bootargs="-m verbose"
zonecfg:firstzone> verify
zonecfg:firstzone> commit
zonecfg:firstzone> exit
```

# 5. Check the status of the virtual NIC.

```
root@solaris:~# dladm show-link
LINK      CLASS  MTU  STATE  OVER
net0      phys   1500 up     --
vboxnet0  phys   1500 up     --
```

# 6. Check the configured status of the zone.

```
root@solaris:~# zoneadm list -cv
ID  NAME        STATUS     PATH           BRAND  IP
0   global      running    /              solaris shared
-   firstzone   configured /zones/firstzone solaris excl
```

7. Install the zone, which we will name firstzone, from an online IPS repository using the zoneadm command. Your computer must be connected to the Internet, and you must have access to an IPS repository. This is a long step (on our system it took about 20 minutes) where you have to wait for the repository packages to load and install.

```
root@solaris:~# zoneadm -z firstzone install
The following ZFS file system(s) have been created:
  rpool/zones
    rpool/zones/firstzone
Progress being logged to /var/log/zones/
zoneadm.20141017T0830492.firstzone.install
  Image: Preparing at /zones/firstzone/root.
  Install Log: /system/volatile/install.3819/install_log
  AI Manifest: /tmp/manifest.xml.MvAWbH
    SC Profile: /usr/share/auto_install/sc_profiles/enable_sci.xml
Zonename: firstzone
Installation: Starting ...
  Creating IPS image
Startup linked: 1/1 done
  Installing packages from:
    solaris
      origin: http://pkg.oracle.com/solaris/release/
DOWNLOAD  PKGS   FILES   XFER (MB)  SPEED
Completed 282/282 53274/53274 351.9/351.9 344k/s
PHASE      ITEMS
Installing new actions 71043/71043
Updating package state database Done
Updating package cache 0/0
```