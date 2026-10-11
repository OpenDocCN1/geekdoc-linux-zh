This is equivalent to issuing the following traditional kernel-building steps:

```
make
make install
make modules
make modules_install
```

As with the previous step, if all went well, you should see the following two lines at the bottom of the screen:

```
make[1]: Leaving directory `/usr/src/linux-2.2.16`
utils/errcheck out.kinstall
```

If you have already built and installed this version of the kernel before (which I strongly recommend), your /etc/lilo.conf file should not need to be modified. Simply rerun the lilo command:

```
[ramon]$ sudo /sbin/lilo
```

Then reboot your system. Upon startup, you should see messages of the type

```
klips_debug:ipsec_tunnel_init: initialisation of device: ipsec0
```

and you should verify that the IKE daemon (pluto) is active:

```
[ramon]$ ps -ef | grep pluto
root 490 1 0 20:43 ? 00:00:00 /usr/local/lib/ipsec/pluto --deb
```

In addition, you may want to make sure that your system now has at least one virtual IPsec interface:

```
[ramon]$ ifconfig ipsec0
ipsec0 Link encap:IPip Tunnel HWaddr
NOARP MTU:0 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame:0
RX packets:0 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:10
```

If everything looks to be in place, go on to the next section and begin configuring your IPsec connections!

# ## Configuring FreeS/WAN

If you have made it this far, your system is currently IPsec enabled and is ready to be configured to establish secure connections with other Linux servers.