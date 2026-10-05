# 7.2. chroot and setuid (for UNIX servers)

On UNIX servers, it is possible to run BIND in a chrooted environment (`chroot()`) by specifying the "-t" option. This can help improve system security by placing BIND in a "sandbox," which will limit the damage if a server is compromised.

Another useful feature in the UNIX version of BIND is the ability to run the daemon as a nonprivileged user (`-u user`). We suggest running as a nonprivileged user when using the chroot feature.

Here is an example command line to load BIND in a chroot() sandbox, `/var/named`, and to run named setuid to 202:

```
/usr/local/bin/named -u 202 -t /var/named
```

# 7.2.1. The chroot Environment

In order for a chroot() to work properly in a particular directory (for example `/var/named`), you will need to set up an environment that includes everything BIND needs to run. From BIND's point of view, `/var/named` is the root of the filesystem. You will need to adjust the values of options like pid-file to account for this.

Unlike earlier versions of BIND, you will not need to compile named statically install shared libraries under the new root. However, depending on your operating system, you may need to set up things like `/dev/zero`, `/dev/random`, `/dev/log`, and/or `/etc/localtime`.

# 7.2.2. Using the setuid Function

Prior to running the named daemon, use the touch utility (to change file access and modification times) or the chown utility (to change the user id and group id) on files to which you want BIND to write. Note that if the named daemon is running as a nonprivileged user, it will not be able to bind to restricted ports if the server is reloaded.

# 7.3. Dynamic Update Security

Access to the dynamic update facility should be strictly limited. In earlier versions of BIND the only way to do this was based on the IP address of the host requesting the update, by listing an IP address or network prefix in the allow-update zone option. This method is insecure because the source address of the update UDP packet can be easily forged. Note that if the IP addresses allowed by the allow-update option include the address of a slave server which performs forwarding of dynamic updates, the master