+   - You have two choices in the `yp.conf` file:
+     - **Configure the ypbind daemon to broadcast for an NIS server for the correct domain:** Include the directive `domain domainname broadcast`. This directive indicates that the client should connect to the specified domain name and broadcast for a server to handle requests.
+     - **Configure the ypbind daemon to connect to a specific NIS server:** Include the directive `ypserver hostname`. This directive is to use a specific host as the NIS server. The hostname and its IP address must be listed in `/etc/hosts` on the client.

# RUNNING ypbind

After the correct configuration has been entered in `/etc/yp.conf`, you need to run ypbind to bind your client to the NIS domain. Do so with the following command:

```
```sh
# /etc/rc.d/init.d/ypbind start
```
```

If ypbind were already running on your system, you would first stop ypbind and then restart it with the above command. To stop ypbind, use the following command:

```
```sh
# /etc/rc.d/init.d/ypbind stop
```
```

# EDITING THE `/etc/passwd` FILE

Once your system is a client on an NIS network, you need to configure it to perform user authentication against your NIS maps. To do this, add the following line to the end of the `/etc/passwd` file:

```
```text
+::::::
```
```

The plus sign tells the system to look up usernames not defined in the local `/etc/passwd` file through NIS.

However, if a user already has an entry in the local `/etc/passwd` file that appears before the + entry, and the `/etc/nsswitch.conf` file is configured to consult the local password file first before consulting the NIS database, this password entry will override the NIS password entry. Refer to the section “Understanding the Name Server Switch” for an explanation of how the `nsswitch.conf` file is used.

Password file overrides should be avoided in general, unless there is a very good reason for a user to have a different UID, GID, home directory, or local password on a specific machine. Maintaining local user accounts on individual machines creates the same administrative overhead that NIS is designed to avoid.