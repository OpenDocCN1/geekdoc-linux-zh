
7. Change the directory to `arch/i386/boot`. If your hardware architecture is Intel, you have to replace `i386` and may also need further instructions from the kernel how-to documentation to compile and install your flavor of the kernel. I assume that the majority of readers' systems are i386-based and continue.

8. Copy `bzImage` to `/boot/vmlinuz-2.4.1` and edit the `/etc/lilo.conf` file to include a new configuration such as the following:
```text
image=/boot/vmlinuz-2.4.1
label=linux3
read-only
root=/dev/hda1
```

9. Run the `/sbin/lilo` command to reconfigure `lilo` and reboot your system. At the `lilo` prompt enter `linux3` and boot the new kernel. If you have any problem, you should be able to reboot to your standard Linux kernel, which should be the default.

10. After you have booted the new kernel, you are now ready to use ramfs. Create a directory called `ramdrive` by using the `mkdir /ramdrive` command.

11. Now mount the ramfs file system with the `mount -t ramfs none /ramdrive` command.

You are all set; you can now write files to `/ramdrive` as usual.

> **Caution**
>
> Be forewarned that when the system is rebooted, or when you unmount the file system, all contents will be lost. This is why it should be a temporary space for high-speed access. Also, note that because ramfs is really not a block device, programs such as `df` and `du` cannot see it. You can verify that you are really using RAM by running the `cat /proc/mounts` command and finding an entry such as the following:
> ```text
> none /ram ramfs rw 0 0
> ```

> **Tip**
>
> You can specify options using `-o` option when mounting the file system, just like mounting a regular drive-based file system. For example, to mount the ramfs file system as read-only, you can use the `-o ro` option. You can also specify special options, such as `maxsize=n` where `n` is number of kilobytes to allocate for the file system in RAM; `maxfiles=n` where `n` is the number of all files allowed in the file system; and `maxnodes=n` where `n` is the maximum number of inodes (default is `0` = no limits).

# Making use of the RAM-based file system

If you run a Web server, you will have many uses for a RAM-based file system. Elements such as common images and files on your Web site that are not too big (no more than a few KB) can be kept in the ramfs file system. You can write a simple shell script to copy the contents from their original location on each reboot. Listing 23-4 is a simple script that does that.

## Listing 23-4: _make_ramfs.sh_

```sh
#!/bin/sh
#
# Simply script to create a ramfs file system
# on $MOUNTPONT (which must exists).
#
# It copies files from $ORIG_DIR to $MOUNTPONT
# and changes ownership of $MOUNTPONT to
# $USER and $GROUP
#
# Change values for these variables to suit
# your needs.

MOUNTPONT=/ram
ORIG_DIR=/www/commonfiles

USER=httd
GROUP=httpd

MOUNTCMD=/bin/mount
CHOWN=/bin/chown
CP=/bin/cp

echo -n "Creating ramfs file system in $MOUNTPONT ":
$MOUNTCMD -t ramfs none $MOUNTPONT
echo "done."

echo -n "Copying $ORIG_DIR to $MOUNTPONT ... ":
$CP -r $ORIG_DIR $MOUNTPONT
echo "done."

echo -n "Changing ownership to $USER:$GROUP for $MOUNTPONT ...":
$CHOWN -R $USER:$GROUP $MOUNTPONT
echo "done."
```

To use this script on your system, do the following:

- 1. Create `make_ramfs.sh` in your `/usr/local/scripts` directory. Create the `/usr/local/scripts` directory if you don't have one.
- 2. Edit `/etc/rc.d/rc.local` file and append the following line to it:
  `/usr/local/scripts/make_ramfs.sh`
- 3. Create a directory called `ram` by using the `mkdir ram` command. If you keep the files you want to load in RAM in any location other than `/www/commonfiles`, then modify the value for the `ORIG_DIR` variable in the script. For example, if your files are in the `/www/mydomain/htdocs/common` directory, then set this variable to point to this directory.
- 4. If you run your Web server by using a username or group other than `httpd`, then change the `USER` and `GROUP` variable values accordingly. For example, if you run Apache as `nobody` (user and group), then set `USER=nobody` and `GROUP=nobody`.
- 5. If you are using Apache Web server, create an alias in your `httpd.conf` file such as the following:

```text
Alias /commonfiles/ "/ram/commonfiles/"
```

Whenever Apache Web server needs to access `/commonfiles/*`, it will now use the version in the RAM, which should be substantially faster than the files stored in the original location. Remember that the RAM-based version will disappear whenever you reboot or unmount the file system. So never update anything there unless you also copy the contents back to a drive-based directory.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_701_0.png)

If you mounted a `ramfs` file system by using a command such as `mount -t ramfs none /ram` and copied contents to it and later reran the same mount command, the rerunning of the same command wipes out the contents and remounts the `ramfs`. The `/proc/mounts` file shows multiple entries for the same mount point, which causes a problem when unmounting the device. If you must regain the memory for another use, you have to reboot. It is hoped that this will be fixed soon.

# Creating a Reliable Back-end Network

A typical Web network consists of a set of Web servers, proxy servers, application servers, database servers, and the like. In most cases, only the Web servers and proxy servers (if any) need to be in the front-end of the Web network. Figure 23-3 shows an example Web network with a front-end and back-end network.

Each Web server node has two network interfaces. One interface is connected to the front-end network `207.185.233.0/24` and the other one is connected to the back-end network `192.168.1.0/24`. The front-end network consists of the Web servers and the load-balancing hardware; the back-end network consists of the Web servers, application servers, and the database servers.

When a request comes to the active (primary) load balancer, the following chain of actions is performed:

- The load balancer determines the best Web server to service the request and passes the request to appropriate Web server.
- The Web server decides whether the request requires any additional resources. For example, if the request is to run an application on the application server, the Web server selects the appropriate application server and/or database server and performs the tasks necessary to complete the request.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_702_0.png)

**Figure 23-3:** A Web network with both front- and back-end network

The application server(s) and database server(s) do not need to be accessible directly via the Web because only the Web servers in the front-end network contact them. This ensures good security and therefore it is a good idea to use a non-routable 192.168.x.x network address for all back-end networks attached to a Web network.

However, a large Web network requires that the application servers and the database servers be load balanced as well, otherwise the application or database usage becomes a major bottleneck for very busy sites. Figure 23-4 shows a highly balanced Web network that uses load-balancing hardware for both front-end and back-end networks.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_703_0.png)

**Figure 23-4:** A Web network with both front-end and back-end load balancers

# Fortifying Your Web Network

Hackers find Web networks or any cluster of nodes that comprise an Internet service to be ideal candidates for attacks. This is because if they can break into a network of computers, the network can be used as a launching pad for attacks on other systems. Basically, a poorly secured, yet well-connected (high bandwidth) Web network provides hackers with a great resource for attacking others. This can result in serious problems for Web network administrators. Therefore, it is critical that you perform all the preventive measures that you can to reduce the risk of being attacked. See Chapter 18 for details on how to secure your Web server. This section provides additional security-related information that is suitable for Web networks, as well as for a single-server system.
