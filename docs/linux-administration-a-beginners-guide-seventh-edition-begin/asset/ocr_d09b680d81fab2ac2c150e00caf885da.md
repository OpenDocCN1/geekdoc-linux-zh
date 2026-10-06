# CHAPTER 6 Booting and Shunting Down

# 175

# Disabling a Service

To disable a service completely, you must, at a minimum, know the name of the service. You can then use the chkconfig (or systemctl) tool to turn it off permanently, preventing it from starting in all runlevels.

For example, to disable our "wist-saving" carpald.sh program, you could type this:

```
[root@fedora-server ~]# chkconfig carpald off
```

If you want to use systemd's systemctl utility to disable the carpald service, type this:

```
[root@fedora-server ~]# systemctl disable carpald
```

If you check the runlevels for the carpald.sh program, you will see that it has been turned off for all runlevels:

```
[root@fedora-server ~]# chkconfig --list carpald
0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

To remove the carpald.sh program permanently from the chkconfig utility's control, use chkconfig's delete:

```
[root@fedora-server ~]# chkconfig --del carpald
```

We are done with our sample carpald.sh script, and to prevent it from flooding us with e-mail notifications (in case we accidentally turn it back on), we delete it from the system for:

```
[root@fedora-server ~]# rm -f /usr/local/bin/carpald.sh
```

And that's how services start up and shut down automatically in Linux. Now go out and take a break.

# Graphical Service Managers

GUI tools are available that will help you manage services start at any runlevel. In Fedora and other Red Hat-type systems (including RHEL and CentOS), one tool is the system-config-services utility (see Figure 6-1). Another is the all-encompassing, web-based Cockpit server manager (http://cockpit-project.org/), which also has a function to manage services using system-config-services program, type the following:

```
[root@fedora-server ~]# system-config-services
```

On a system running OPENSE Linux, the equivalent GUI program (see Figure 6-3) can be launched by typing this:

```
opensuse-server:~ # yast2 services-manager
```