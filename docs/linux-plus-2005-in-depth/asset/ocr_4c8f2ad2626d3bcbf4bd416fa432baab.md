+   8. Generate the configuration file maps by typing `/usr/lib/yp/ypinit` -m at a command prompt.
+   9. Allow clients to connect by typing `ypbind` at a command prompt.

Setting up the NIS Client:

+   1. Define the NIS domain name by typing the command `domainname NIS_domain_name` at a command prompt.
+   2. Add the following line to `/etc/sysconfig/network` to configure the NIS domain from Step 1 at every boot time:
+      NISDOMAIN="NIS_domain"
+   3. Edit the `/etc/yp.conf` file and add the following line to query a specific NIS server:
+      domain NIS_domain server NIS_server

Alternatively, you can add the following line to listen for NIS broadcasts on the network:
domain NIS_domain broadcast

+   1. Start the NIS client program by typing `ypbind` at a command prompt.
+   2. Locate the NIS server by typing the command `ypwhich` at a command prompt.
+   3. Add the following line to `/etc/passwd` to redirect all requests to the NIS server:
+      +:::0:0:::

After the NIS server and client have been set up, ensure that all users on NIS clients use the `ypasswd` command to change their NIS password; using the `passwd` command only modifies the local password database.

![](bbox=[0.18, 0.62, 0.3, 0.66])

> NIS was originally called Yellow Pages; as a result, many configuration commands and files are prefixed with the letters yp.

# Configuring the Secure Shell Daemon

The Secure Shell daemon (sshd) allows you the ability to use the `ssh` utility to log in to a server across the network in a secure manner and receive a BASH shell that can be used to run applications or monitor the server. The configuration file that specifies the options used by the ssh daemon is called `/etc/ssh/ssh_config`. Most of this file is commented, and should only be edited to change the default settings that the ssh daemon uses when servicing ssh clients. The most common options that are changed in this file are those that deal with authentication and encryption.