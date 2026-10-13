+   @Anonymous FTP Server
+   @Web Server
+   @Development
+   @Kernel Development
+   @Utilities

A complete list of groups and individual packages is in the file RedHat/base/comps on the Red Hat Linux installation CD-ROM.

# POST-INSTALLATION SECTION

The post-installation section starts with the keyword `$post`. You can add any post installation tasks here, including additional packages to be added with the `rpm`, custom startup scripts to be run, crontab entries to be added, and any other necessary tasks.

A sample post-installation section is shown here. It shows how startup commands can be added to the `/etc/rc.local` file and how to add a new entry to root account’s crontab:

```
```text
%post
cat <<EOF >>/etc/rc.local
echo 8192 > /proc/sys/kernel/file-max
echo 32768 > /proc/sys/kernel/inode-max
EOF
cat <<EOF >/tmp/crontab.root
# Keep all the time up to date
0,15,30,45 * * * * /usr/sbin/ntpdate -s eqtimer 2>&1 >/dev/null
```
```

Basically, the post-installation section consists of a shell script to be executed after the system is installed and functional. Commands here should be specified as they would be in a shell script. Be aware, it is not possible to have any interactive installation actions in the post-installation section of Kickstart.

**INSTALLING CUSTOM PACKAGES** You can install your own RPM packages by adding rpm install commands in the post-installation section of the Kickstart configuration file. For instance, suppose that you have two custom packages called `sudo.rpm` and `ssh.rpm` placed in the `/kickstart/RPMS` directory on the NFS server you are using for network installation of the Linux software. You can arrange for these packages to be automatically installed by adding directives in the post-installation section of the configuration file as follows:

```
```text
%post
rpm -i /kickstart/RPMS/sudo.rpm
rpm -i /kickstart/RPMS/ssh.rpm
```
```

The post-installation commands are executed after the operating system is completely installed and the system is fully functional. The two rpm commands shown will execute and the sudo and ssh packages will be automatically installed.