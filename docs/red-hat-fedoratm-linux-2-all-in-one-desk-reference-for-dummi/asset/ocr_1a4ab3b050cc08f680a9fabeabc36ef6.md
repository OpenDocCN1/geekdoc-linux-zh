of these services depends on factors such as how the system connects to the Internet and how the system is being used. You can usually turn off most `xinetd` services.

Check which `xinetd` services are turned on by using one of the following ways:

+   ◆ Check the configuration files in the `/etc/xinitd.d` directory for all the services that `xinetd` can start. If a service is turned off, the configuration file has a line like this:
+   
+   disable = yes
+   
+   *Remember:* The `disable = yes` line doesn't count if it's commented out by placing a `#` at the beginning of the line.

+   ◆ Type the following command to disable a service that `xinetd` can start:
+   
+   chkconfig servicename off
+   
+   where *servicename* is the name of the service (such as `telnet` or `sgi_fam`). To check the names of the services that `xinetd` can start, type the following command:
+   
+   chkconfig --list | more
+   
+   In the output, look for the lines that follow:
+   
+   `xinetd` based services:
+   
+   These lines list all the services that `xinetd` can start and whether they are on or off. For example, here are a few lines showing the status of `xinetd` services on a system:
+   
+   telnet: on
+   sgi_fam: on
+   echo-udp: off
+   chargen: off
+   cups-lpd: off
+   services: off
+   finger: off
+   ... lines deleted ...

In this case, `telnet` (a server that enables users to remotely log in to the system) and `sgi_fam` (a server that reports changes to any file) services are on, but everything else is off.

Also check the following files for any access controls used with the `xinetd` services:

+   ◆ `/etc/hosts.allow` lists hosts allowed to access specific services.
+   ◆ `/etc/hosts.deny` lists hosts denied access to services.