```
194436 bytes received in 22.7 secs (8.4 Kbytes/sec)
ftp> quit
221-You have transferred 194436 bytes in 1 files.
221-Total traffic for this session was 197280 bytes in 2 transfers.
221-Thank you for using the FTP service on wareZ.zedz.net.
221 Goodbye.
```

```
[ramon]$ sudo rpm -i cfs-1.3_bf-1.1386.rpm
```

At this point you have installed CFS on your system (note that there is no need to rebuild the kernel or reboot the server). Let's take a look at configuring CFS in the next step.

# ### Configuring CFS

The first step is to make sure your server is configured to run NFS services (statd, portmapper, and mountd). This is a requirement for CFS to work correctly. Since CFS actually protects the privacy of NFS shares, perhaps this is just the tool you were looking for to add NFS back into your security policy. You can verify that NFS is running on your system by looking for the mountd line with the following command:

```
[ramon]$ ps aux | grep mountd
        5756  0.0  0.7  1132  456 ?  S   19:15  0:00 rpc.mountd
```

Next, create a /nu11 directory. CFS refers to this directory as the bootstrap mount point. In addition, you need to create the directory that you want to use as the root for all encrypted data (I chose /crpyt for this purpose):

```
[ramon]$ sudo mkdir /nu11
[ramon]$ sudo chmod 0000 /nu11
[ramon]$ sudo mkdir /crpyt
```

Add the /nu11 directory to the list of exported filesystems using the following command:

```
[ramon]$ echo "/nu11 localhost" >> /etc/exports
```

Add the following commands to the end of /etc/rc.d/rc.local:

```
if [ -x /usr/sbin/cfso ]; then
       /usr/sbin/cfso
       /bin/mount -o port=3049,intr localhost:/nu11 /crpyt
fi
```

That's the end of the installation. You're now ready to try out CFS. You can either restart your system or type the commands that you just added in the rc.local file by hand.