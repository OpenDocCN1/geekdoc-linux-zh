Once the configuration script has completed, build and install the Net-SNMP components:

```
$ make
$ make install
```

The SNMP agent executable built by default by Net-SNMP seems like a rather small binary. If you compile it against glibc and strip it, it will measure a measly 24 KB when linked dynamically. However, much of the code resides in dynamic libraries that are built together with the executable and are needed for its proper operation at runtime. Together with these libraries, the total space taken by the SNMP agent is a whopping 1276 KB. If you compile it against uClibc and strip it, it will measure 625 KB. Because the figures for the unstripped binaries all exceed 1.7 MB, we strongly encourage you to strip the agent binary.

The complete build and installation will take around 10 minutes, depending on your hardware, because Net-SNMP is quite a large package. In addition to copying binaries, the installation copies manpages and headers into the $[TARGET_PREFIX] directory. The SNMP daemon (snmpd), which is the actual SNMP agent, is installed in $[TARGET_PREFIX]/sbin. The dynamic libraries built during the build and required by the binary reside in $[TARGET_PREFIX]/libs. The other SNMP utilities, such as snmpget, are installed in $[TARGET_PREFIX]/bin. The SNMP trap daemon is also installed in $[TARGET_PREFIX]/sbin (this daemon is used to monitor incoming traps). The MIB information required by the SNMP daemon is installed in $[TARGET_PREFIX]/share/snmp.

With all the Net-SNMP components installed in your development workspace on the host, copy the SNMP daemon, and dynamic libraries to your target’s root filesystem:

```
$ cp $[TARGET_PREFIX]/sbin/snmpd $[PRJROOT]/rootfs/usr/sbin
$ cp -a $[TARGET_PREFIX]/libs/*libnetsnmp*.so* $[PRJROOT]/rootfs/usr/lib
```

Copy the relevant components found in $[TARGET_PREFIX]/share/snmp to the /usr/local/share/snmp directory of your target’s root filesystem:

```
$ mkdir -p $[PRJROOT]/rootfs/usr/local/share
$ cp -r $[TARGET_PREFIX]/share/snmp $[PRJROOT]/rootfs/usr/local/share
```

To run properly, the SNMP agent requires a configuration file. An example configuration (EXAMPLE.conf) was created during the build of the Net-SNMP package in the package’s root directory. Customize that file and copy it to your $[PRJROOT]/rootfs/usr/local/share/snmp directory:

```
$ cp EXAMPLE.conf $[PRJROOT]/rootfs/usr/local/share/snmp/snmpd.conf
```

Finally, edit your target’s /etc/inittab file to add a line for snmpd. Here is the line we added for snmpd in our SYSM module’s inittab:

```
::respawn:/usr/sbin/snmpd -f
```

The -f option instructs snmpd not to fork from the calling shell. In other words, snmpd will not become a daemon and init will respawn it if it dies.