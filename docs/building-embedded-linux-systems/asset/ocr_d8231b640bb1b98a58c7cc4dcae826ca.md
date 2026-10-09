In addition to using the options offered by the configure script, you can also edit the options.h include file directly, removing some unneeded ciphers and check codes (such as MD5) as a way to produce a smaller runtime binary.

![](bbox=[0.17, 0.16, 0.25, 0.24])

If you disable zlib support, you must explicitly disable compression support in the client side. Certain versions of the commonly used OpenSSH client are possibly buggy in this regard, so disable compressions support globally (not just for the particular host) in ~/.ssh/config by adding the 'Compression off' keyword.

In addition, you may want to disable lastlog recording when using uClibc if uClibc was not built with lastlog support. This can be done by providing the `--disable-lastlog` switch to the configure script.

Last but not least, note that the tips regarding the pseudoterminal interface presented in the section about the netkit-telnetd daemon apply also to the SSH service and Dropbear.

Next, we’ll build the package, which combines the SSH server itself, the scp utility (which performs secure file transfer on top of the SSH secure channel), and the dropbearkey utility, (which allows you to compute a unique key for your target during its first boot). The DESTDIR build variable denotes the location to which the install target will copy the generated binary.) We will use a nice feature that the Dropbear package offers that lets us build a single binary executable for all three programs, which will produce a smaller footprint for the SSH server. In addition, we will strip the binary.

```
$ make PROGRAMS="dropbear dropbearkey scp" --prefix=/usr\
>            MULTi=1 DESTDIR=$\{TARGET_PREFIX\} strip install
```

The generated multiprogram binary, called dropbearmulti (241 KB in size) needs to be copied to its location on the root filesystem. We will need to create symbolic links that link the names of the three different programs we have created to the actual binary:

```
$ cp ${TARGET_PREFIX}/usr/bin/dropbearmulti \\
>    ${PRJROOT}/rootfs/usr/bin/dropbear
$ ln -s ../sbin/dropbear ${PRJROOT}/rootfs/usr/bin/dropbearkey
$ ln -s ../sbin/dropbear ${PRJROOT}/rootfs/usr/bin/scp
```

Now, edit your target’s /etc/inittab file to add a line for starting the dropbear daemon at boot. Here is the line we added for Dropbear in our SYSM module’s inittab. As you might recall, the `respawn` directive tells init to run the specified program (dropbear, in our case) and restart it if it ever terminates:

```
::respawn:/usr/sbin/dropbear -f -d /etc/dropbear_dsa_host_key
::t /etc/dropbear_rsa_hos_key
```

We are not done yet, however. When the dropbear daemon starts, it will look for two files: one containing an RSA cryptographic key, the other a DSA key. The keys are used to identify the target to SSH clients connecting to it and are part of the SSH protocol